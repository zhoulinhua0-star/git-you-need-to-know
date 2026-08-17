# 6. 远程仓库（Remote）

Remote 是指向另一个仓库的具名连接，让不同仓库能够交换 commits；它不是工作区的实时副本。

```text
本地 main  ──push──→  服务器上的 origin/main
    ↑                         │
    └──── merge/rebase ── fetch
```

## 三种名字

| 名字 | 含义 |
| --- | --- |
| `main` | 你的本地 branch |
| `origin` | 已配置的 remote 仓库 |
| `origin/main` | 本地保存的远程 `main` branch 状态记录 |

`origin/main` 只会在你与 `origin` 通信时更新，并不会持续自动同步。

## 检查并同步

```bash
git remote -v
git fetch origin
git status
```

`git fetch` 下载 commits，并更新 remote-tracking branches。它不会改变工作区或本地 branch。

下载后，可以有意识地整合远程工作：

```bash
git merge origin/main
```

也可以使用便捷命令：

```bash
git pull --ff-only
```

`git pull` 会先执行 `fetch`，再执行整合。`--ff-only` 只允许 Git 通过移动 branch 完成快进；如果需要创建 merge commit 或执行 rebase，则操作失败。

发布新 branch，并设置其 upstream：

```bash
git push -u origin docs/staging
```

此后，直接运行 `git push` 和 `git pull` 就知道应该使用哪个远程 branch。

> 想先检查远程历史时，先 fetch，再决定如何整合。Remote 是协作边界，不是未提交工作的备份。

---

[← 上一章：分支（Branch）](05-branch.md) · [下一章：合并（Merge）→](07-merge.md)
