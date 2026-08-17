# 9. 变基（Rebase）

Rebase 会把 commits 复制到一个新的基点上。历史因此可以变得线性，但复制出的 commits 会拥有新的身份。

```text
变基前：     C──D  ← topic
            /
       A──B──E  ← main

变基后：A──B──E──C'──D'  ← topic
```

`C'` 和 `D'` 包含与 `C`、`D` 类似的改动，但它们拥有新的 hash 和父 commits，因此是新的 commits。

## 更新本地 topic branch

```bash
git fetch origin
git switch topic
git rebase origin/main
```

如果重放过程因冲突暂停：

```bash
# 解决文件冲突，然后：
git add <resolved-paths>
git rebase --continue
```

放弃整个 rebase：

```bash
git rebase --abort
```

## 交互式整理

分享本地工作前，可以用 interactive rebase 调整最近 commits 的顺序、合并 commits、修改内容或重写提交消息：

```bash
git rebase -i HEAD~3
```

仔细阅读 todo 列表。每个被修改的 commit 以及它之后的所有后代，都会获得新的 hash。

## 公开历史原则

> **不要随意 rebase 其他人可能已经基于其工作的 commits。**重写共享历史，会迫使协作者处理同一段历史的两个版本。

Rebase 只有自己使用、尚未分享的 topic branch 通常是安全的。Rebase 共享 branch 前，必须与团队明确协调。

如果 rebase 后的 branch 之前已经发布，更新远程 branch 可能需要：

```bash
git push --force-with-lease
```

这会重写远程 branch。`--force-with-lease` 增加了一道安全检查，但它仍然会破坏共享历史。除非重写是有意且已协调的，否则优先使用普通 push。

---

[← 上一章：冲突（Conflict）](08-conflict.md) · [下一章：撤销与恢复 →](10-undo.md)
