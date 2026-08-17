# 5. 分支（Branch）

Branch 是一个指向 commit、并且可以移动的名字。创建 branch 的成本很低，因为 Git 不会复制项目历史。

```text
        C  ← docs/staging
       /
A──B──D  ← main
```

`HEAD` 通常指向当前 branch。Commit 时，当前 branch 会向前移动，其他 branches 保持不动。

## 开始一项并行工作

```bash
git switch -c docs/staging
# 编辑、暂存并提交
git add docs/03-staging-area.md
git commit -m "说明如何暂存部分改动"
```

`git switch -c` 会在当前 commit 创建 branch 并切换过去。之后可以运行：

```bash
git switch main
git branch --list
```

工作区会改变为所选 branch 对应的内容。如果未提交的修改可能被覆盖，Git 会拒绝切换。此时应先 commit、stash，或明确地丢弃改动。

## 用目的命名 branch

好的名字能说明这项工作的内容：

```text
docs/staging-example
fix/broken-navigation
```

删除已经完整合并的本地 branch：

```bash
git branch -d docs/staging
```

`-d` 会检查 branch 是否已经合并。大写的 `-D` 会强制删除，可能让尚未合并的 commits 更难找回。

> Branch 不会隔离未提交的改动。这些改动位于工作区，切换 branch 时可能会跟着你移动。

---

[← 上一章：提交（Commit）](04-commit.md) · [下一章：远程仓库（Remote）→](06-remote.md)
