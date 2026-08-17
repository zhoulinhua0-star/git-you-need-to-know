# Git 速查表

当你知道目标、却忘了命令时，使用这张表。想理解每个操作背后的模型，请阅读对应章节。对 `-c`、`-m`、`-u` 等写法有疑问时，请阅读 [Git 命令行选项科普](git-command-options.md)。

## 检查状态与历史

```bash
git status                              # 当前 branch 与文件状态
git diff                                # 未暂存的改动
git diff --staged                       # 已暂存的改动
git log --oneline --graph --decorate    # 紧凑的历史图
git show <commit>                        # 某个 commit 及其 patch
```

## 创建或复制仓库

```bash
git init
git clone <url>
```

详见[仓库](docs/02-repository.md)。

## 暂存下一个快照

```bash
git add <path>                  # 按完整路径暂存
git add -p <path>               # 逐个选择改动片段
git restore --staged <path>     # 取消暂存，保留工作区改动
```

详见[工作区与暂存区](docs/03-staging-area.md)。

## 提交

```bash
git commit -m "说明这个改动"
git show HEAD
```

详见[提交（Commit）](docs/04-commit.md)。

## 使用 branches

```bash
git branch --list
git switch -c <new-branch>
git switch <branch>
git branch -d <merged-branch>
```

详见[分支（Branch）](docs/05-branch.md)。

## 与 remote 同步

```bash
git remote -v
git fetch <remote>
git pull --ff-only
git push
git push -u origin <branch>
```

详见[远程仓库（Remote）](docs/06-remote.md)。

## 整合工作

```bash
git merge <branch>
git merge --ff-only <branch>
git rebase <new-base>
git cherry-pick <commit>
```

详见[合并（Merge）](docs/07-merge.md)和[变基（Rebase）](docs/09-rebase.md)。

## 解决或取消冲突

```bash
git status
git add <resolved-paths>
git merge --abort
git rebase --continue
git rebase --abort
git cherry-pick --abort
```

详见[冲突（Conflict）](docs/08-conflict.md)。

## 安全撤销

```bash
git restore <path>                  # 丢弃未暂存改动：Git 通常无法恢复
git restore --staged <path>         # 取消暂存，保留改动
git revert <commit>                 # 创建新 commit，安全地反转历史
git reset --soft HEAD~1             # 移除本地 commit，改动继续暂存
```

> `git reset --hard <commit>` 会移动 branch，并丢弃已跟踪文件的改动。只有确定要失去这些内容时才使用。

详见[撤销与恢复](docs/10-undo.md)。

## 恢复历史

```bash
git reflog
git branch recovery <commit>
git fsck --lost-found                # 最后的手段：搜索不可达对象
```

Reflog 只存在于本地，而且有时效。找到 commit 后，应立即创建 branch。

## 暂时收起工作

```bash
git stash push -m "WIP：工作说明"
git stash list
git stash pop
```

详见[Git 进阶](docs/12-advanced.md)。

---

[返回 README](README.md) · [理解命令行选项](git-command-options.md)
