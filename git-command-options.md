# Git 命令行选项：`-c`、`-m`、`-u` 到底是什么？

`-c`、`-m`、`-u` 不是 Bash 语言，而是 **Git 命令行选项（options，也常叫 flags）**。

最重要的一点是：**选项属于它前面的 Git 层级或子命令。脱离完整命令谈 `-c`，通常没有唯一答案。**

```bash
git -c color.ui=false status     # Git 全局层级：临时设置一项配置
git switch -c docs/options       # switch 子命令：创建并切换 branch
git commit -c HEAD~1             # commit 子命令：复用并编辑某个 commit 的消息
```

同一个 `-c`，在三个位置中有三种不同含义。

## 一条 Git 命令的结构

```text
git [Git 全局选项] <子命令> [子命令选项] [--] [参数]
│        │          │           │        │     │
程序   影响本次 Git   要执行的动作   调整动作    分隔符  操作对象
```

例如：

```bash
git -C ../handbook commit -m "补充命令行选项" -- README.md
```

| 部分 | 含义 |
| --- | --- |
| `git` | 启动 Git |
| `-C ../handbook` | 先把工作目录切换到 `../handbook` |
| `commit` | 执行 commit 子命令 |
| `-m "补充命令行选项"` | 直接提供提交消息 |
| `--` | 后面的内容只作为参数，不再解析成选项 |
| `README.md` | 本次命令处理的路径 |

## 短选项、长选项与参数

许多 Git 选项同时有短写和长写：

```bash
git commit -m "补充说明"
git commit --message "补充说明"
```

二者含义相同。短选项适合频繁输入；长选项更容易阅读。

有些选项不需要值：

```bash
git log --oneline
git add --all
```

有些选项后面必须跟值：

```bash
git commit -m "消息"       # -m 的值是“消息”
git log -n 5               # -n 的值是 5
git config --get user.name # --get 的值是 user.name
```

不需要值的短选项有时可以合并：

```bash
git commit -am "修正文档"  # 等价于 -a -m "修正文档"
git clean -fd              # 等价于 -f -d
```

初学时建议分开写，尤其是危险命令。选项需要值时，紧凑写法也更容易误读。

## `--`：停止解析选项

`--` 表示「后面全部是普通参数」。当 branch 或文件名以 `-` 开头，或名称可能和选项混淆时，它尤其重要。

```bash
git restore -- -draft.md
git log -- docs/10-undo.md
```

第二条命令中的 `--` 明确表示：`docs/10-undo.md` 是路径，不是 revision。

## 最容易混淆的三个字母

### `-c`

| 完整命令 | 含义 |
| --- | --- |
| `git -c name=value <command>` | 只为本次 Git 调用临时设置配置 |
| `git switch -c <branch>` | 创建并切换到新 branch |
| `git commit -c <commit>` | 复用指定 commit 的作者信息和消息，并打开编辑器 |

注意大写 `-C` 也可能不同：

```bash
git -C <path> status       # 在指定目录运行 Git
git switch -C <branch>    # 强制创建或重置 branch，再切换
git commit -C <commit>    # 复用消息，不打开编辑器修改
```

Git 选项区分大小写。`-c` 与 `-C` 不是同一个选项。

### `-m`

| 完整命令 | 含义 |
| --- | --- |
| `git commit -m <message>` | 指定 commit 消息 |
| `git tag -m <message> <tag>` | 指定 annotated tag 消息 |
| `git merge -m <message> <branch>` | 指定 merge commit 消息 |
| `git revert -m <parent> <merge-commit>` | 指定 merge commit 的主线父 commit 编号 |
| `git switch -m <branch>` | 尝试用三方合并保留本地修改并切换 branch |

> `git revert -m 1` 中的 `-m` 是 **mainline**，不是 message。这是一个典型的上下文差异。

### `-u`

| 完整命令 | 含义 |
| --- | --- |
| `git push -u origin <branch>` | push 后设置 upstream |
| `git add -u` | 暂存已跟踪文件的修改和删除，不加入新文件 |
| `git status -u` | 控制未跟踪文件的显示方式 |
| `git commit -u[<mode>]` | 控制预览中未跟踪文件的显示方式 |
| `git stash -u` | stash 时包含未跟踪文件 |

## Git 自身的常用全局选项

这些选项放在子命令之前：

| 选项 | 作用 | 示例 |
| --- | --- | --- |
| `-C <path>` | 在指定目录运行 | `git -C ../project status` |
| `-c <name>=<value>` | 本次调用临时覆盖配置 | `git -c color.ui=false diff` |
| `-p` / `--paginate` | 使用分页器显示输出 | `git -p log` |
| `-P` / `--no-pager` | 禁用分页器 | `git --no-pager log -n 3` |
| `--git-dir=<path>` | 指定 `.git` 目录 | 主要用于特殊布局和诊断 |
| `--work-tree=<path>` | 指定工作区 | 主要用于特殊布局和诊断 |
| `--bare` | 把仓库视为 bare repository | 常见于服务器端仓库 |
| `-v` / `--version` | 显示 Git 版本 | `git --version` |
| `-h` / `--help` | 显示帮助 | `git --help` |

全局 `-c` 只影响这一条命令，不会写入配置文件：

```bash
git -c user.name="临时名字" commit -m "一次性身份示例"
```

## 常用子命令选项

下面列出的是高频选项，不是 Git 全部选项。每个子命令还有更多专用能力。

### 检查状态与历史

| 命令 | 常用选项 | 作用 |
| --- | --- | --- |
| `git status` | `-s` / `--short` | 紧凑输出 |
| `git status` | `-b` / `--branch` | 显示 branch 信息 |
| `git log` | `--oneline` | 每个 commit 显示一行 |
| `git log` | `-n <数量>` | 只显示最近若干 commits |
| `git log` | `-p` / `--patch` | 显示每个 commit 的 diff |
| `git log` | `--stat` | 显示文件修改统计 |
| `git log` | `--graph` | 绘制文本历史图 |
| `git log` | `--all` | 遍历所有 refs |
| `git diff` | `--staged` | 比较暂存区与 `HEAD` |
| `git diff` | `--stat` | 只显示修改统计 |
| `git diff` | `--name-only` | 只显示文件名 |
| `git show` | `-s` / `--no-patch` | 只显示对象信息，不显示 patch |

### 暂存与提交

| 命令 | 常用选项 | 作用 |
| --- | --- | --- |
| `git add` | `-p` / `--patch` | 逐个选择 hunk |
| `git add` | `-A` / `--all` | 暂存所有新增、修改和删除 |
| `git add` | `-u` / `--update` | 只更新已跟踪文件 |
| `git add` | `-n` / `--dry-run` | 预览，不实际暂存 |
| `git add` | `-f` / `--force` | 强制加入被 ignore 的文件 |
| `git commit` | `-m <消息>` | 直接提供提交消息 |
| `git commit` | `-a` / `--all` | 自动暂存已跟踪文件的修改和删除 |
| `git commit` | `--amend` | 重写最后一个 commit |
| `git commit` | `-v` / `--verbose` | 在编辑器模板中显示 diff |
| `git commit` | `-n` / `--no-verify` | 跳过 hooks |

> `git commit -a` 不会加入未跟踪的新文件。`--amend` 会改变 commit hash；已经分享后不要随意使用。

### Branch 与切换

| 命令 | 常用选项 | 作用 |
| --- | --- | --- |
| `git branch` | `-a` / `--all` | 列出本地和 remote-tracking branches |
| `git branch` | `-r` / `--remotes` | 只列出 remote-tracking branches |
| `git branch` | `-d` / `--delete` | 删除已合并的 branch |
| `git branch` | `-D` | 强制删除 branch |
| `git branch` | `-m` / `--move` | 重命名 branch |
| `git branch` | `-vv` | 显示 upstream 与领先/落后信息 |
| `git switch` | `-c <branch>` | 创建并切换 branch |
| `git switch` | `-C <branch>` | 强制创建或重置后切换 |
| `git switch` | `-d` / `--detach` | 进入 detached `HEAD` |

> `-D` 和 `switch -C` 都可能让原有 branch 上的 commits 失去易于查找的名字。操作前先检查历史。

### Remote 与同步

| 命令 | 常用选项 | 作用 |
| --- | --- | --- |
| `git remote` | `-v` / `--verbose` | 显示 remote URL |
| `git fetch` | `--all` | 获取所有 remotes |
| `git fetch` | `-p` / `--prune` | 清理远程已删除的 tracking refs |
| `git pull` | `--ff-only` | 只允许 fast-forward |
| `git pull` | `--rebase` | fetch 后使用 rebase 整合 |
| `git push` | `-u` / `--set-upstream` | 设置 upstream |
| `git push` | `--tags` | 推送所有 tags |
| `git push` | `-d` / `--delete` | 删除远程 ref |
| `git push` | `-n` / `--dry-run` | 预览 push |
| `git push` | `--force-with-lease` | 带安全检查地强制更新 |
| `git push` | `-f` / `--force` | 强制更新远程历史 |

> 优先使用 `--force-with-lease`，不要随意使用 `-f`。二者都会重写远程 branch，只是前者会检查远程是否出现了你未见过的新提交。

### Merge、Rebase 与冲突流程

| 命令 | 常用选项 | 作用 |
| --- | --- | --- |
| `git merge` | `--ff-only` | 只允许 fast-forward |
| `git merge` | `--no-ff` | 即使能 fast-forward，也创建 merge commit |
| `git merge` | `--squash` | 把改动放入工作区和暂存区，不创建 merge commit |
| `git merge` | `--abort` | 取消正在进行的 merge |
| `git rebase` | `-i` / `--interactive` | 交互式整理 commits |
| `git rebase` | `--onto <新基点>` | 精确指定新的基点 |
| `git rebase` | `--continue` | 解决冲突后继续 |
| `git rebase` | `--skip` | 跳过当前正在重放的 commit |
| `git rebase` | `--abort` | 取消整个 rebase |
| `git cherry-pick` | `-n` / `--no-commit` | 应用改动但暂不 commit |
| `git cherry-pick` | `-x` | 在消息中记录来源 commit |

### 撤销、清理与恢复

| 命令 | 常用选项 | 作用 |
| --- | --- | --- |
| `git restore` | `--staged` | 恢复暂存区，保留工作区修改 |
| `git restore` | `-p` / `--patch` | 交互式选择要恢复的 hunk |
| `git reset` | `--soft` | 移动 branch，保留暂存区与工作区 |
| `git reset` | `--mixed` | 移动 branch 并重置暂存区，保留工作区 |
| `git reset` | `--hard` | 移动 branch，并重置暂存区与已跟踪文件 |
| `git revert` | `-n` / `--no-commit` | 应用反向改动但暂不 commit |
| `git clean` | `-n` / `--dry-run` | 预览将删除的未跟踪文件 |
| `git clean` | `-d` | 同时处理未跟踪目录 |
| `git clean` | `-f` / `--force` | 真正执行删除 |
| `git stash` | `-u` / `--include-untracked` | 包含未跟踪文件 |
| `git stash` | `-p` / `--patch` | 交互式选择改动 |

> **危险区域：**`reset --hard`、`clean -f` 和强制 push 都可能造成数据或共享历史丢失。先运行 `git status`；`clean` 先用 `-n` 预览；不确定时先创建临时 branch。

### Tag、搜索与定位

| 命令 | 常用选项 | 作用 |
| --- | --- | --- |
| `git tag` | `-a` / `--annotate` | 创建 annotated tag |
| `git tag` | `-m <消息>` | 指定 tag 消息 |
| `git tag` | `-d` / `--delete` | 删除本地 tag |
| `git tag` | `-l` / `--list` | 按模式列出 tags |
| `git grep` | `-n` / `--line-number` | 显示行号 |
| `git grep` | `-i` / `--ignore-case` | 忽略大小写 |
| `git blame` | `-L <范围>` | 只查看指定行范围 |
| `git bisect` | `start` / `good` / `bad` / `reset` | 二分定位问题 commit；这些是子命令参数，不是短选项 |

## 为什么不应该背一张「全部选项」表

Git 有大量子命令，每个子命令又有独立选项；版本升级还可能增加新能力。同一个字母在不同子命令中可以有不同意思。因此，最可靠的方法是先确定完整命令，再查看该命令的帮助。

```bash
git <command> -h          # 终端中显示简明用法
git help <command>        # 打开完整手册
git help -a               # 列出全部可用子命令
git help -g               # 列出概念指南
```

例如：

```bash
git push -h
git help rebase
git help revisions
git help gitglossary
```

阅读 usage 行时，常见符号含义如下：

| 写法 | 含义 |
| --- | --- |
| `[option]` | 可选内容 |
| `<value>` | 需要替换的值 |
| `A \| B` | 二选一 |
| `...` | 可以重复 |
| `[--] [<pathspec>...]` | 可选的路径参数列表 |

## 记忆方法

不要只记「`-u` 等于什么」，而要记完整短语：

```text
git push -u      → 设置 upstream
git add -u       → 更新已跟踪文件
git stash -u     → 包含未跟踪文件
```

遇到陌生选项时，依次问：

1. 它位于子命令之前还是之后？
2. 它属于哪个子命令？
3. 大小写是否准确？
4. 它是否需要一个值？
5. 它会只读检查、修改文件、移动 branch，还是重写历史？
6. 能否先使用 `--dry-run` 或更安全的替代选项？

掌握这套阅读方式，比背下所有字母更重要。

---

[返回 README](README.md) · [打开 Git 速查表](cheatsheet.md) · [阅读心智模型](docs/01-mental-model.md)
