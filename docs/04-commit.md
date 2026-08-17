# 4. 提交（Commit）

Commit 会记录暂存区中的快照，并把它接入项目历史。

```text
A──B──C
      ↑
 main 上的 HEAD
```

每个 commit 都包含 hash、快照、父 commit、作者和提交者身份、时间戳及提交消息。

## 记录一个完整、单一的改动

```bash
git diff --staged
git commit -m "解释暂存区的作用"
```

提交消息应该说明这个快照为什么存在。推荐使用简短的祈使句，使其可以接在「应用这个 commit 将会……」之后。

```text
好：解释暂存区的作用
差：更新
```

配置未来 commits 中记录的身份：

```bash
git config --global user.name "Ada Lovelace"
git config --global user.email "ada@example.com"
```

这份身份只是 commit 元数据，并不等同于 GitHub 身份验证。

## 查看历史

```bash
git log --oneline --decorate --graph
git show HEAD
git show --stat HEAD
```

`HEAD` 标识当前检出的 commit。正常提交后，当前 branch 与 `HEAD` 都会移到新的 commit。

```text
提交前：A──B     ← main, HEAD
提交后：A──B──C  ← main, HEAD
```

一个 commit 应该小到容易审查，也应该完整到足以让项目保持有意义的状态。在 push 之前，它只存在于本地。

---

[← 上一章：工作区与暂存区](03-staging-area.md) · [下一章：分支（Branch）→](05-branch.md)
