# 10. 撤销与恢复

选择撤销命令前，先回答两个问题：**错误位于哪里？它是否已经分享出去？**

| 需求 | 命令 | 对历史的影响 |
| --- | --- | --- |
| 丢弃某个文件未暂存的修改 | `git restore <path>` | 无 |
| 取消暂存但保留修改 | `git restore --staged <path>` | 无 |
| 反转已经共享的 commit | `git revert <commit>` | 新增一个 commit |
| 把本地 branch 移到另一个 commit | `git reset [mode] <commit>` | 重写该 branch 的历史 |
| 找回引用以前指向的 commit | `git reflog` | 只读检查 |

## 恢复文件

```bash
git restore notes.md
```

这会用暂存区中的版本替换 `notes.md` 未暂存的改动。这些未暂存改动通常无法通过 Git 找回。

```bash
git restore --staged notes.md
```

这会把文件移出下一次 commit，同时保留工作区中的修改。

## 反转共享历史

```bash
git revert a1b2c3d
```

Revert 会创建一个新 commit，应用指定 commit 的反向修改。已有历史保持不变，因此它通常是撤销已发布 commit 的正确选择。

## Reset 本地历史

Reset 会移动当前 branch。Mode 决定暂存区与工作区会发生什么。

| Mode | 暂存区 | 工作区 |
| --- | --- | --- |
| `--soft` | 保留 | 保留 |
| `--mixed`（默认） | 重置 | 保留 |
| `--hard` | 重置 | 重置 |

```bash
git reset --soft HEAD~1
```

这会移除最后一个本地 commit，但把其中的改动继续保留在暂存区。

> **危险：**`git reset --hard` 会丢弃已跟踪文件在工作区中的修改。使用前确认 `git status`、目标 commit，以及这段工作是否已经分享。

## 找回丢失的 commit

Reflog 记录本地引用最近曾经指向的位置：

```bash
git reflog
git branch recovery <commit-hash>
```

找到目标 commit 后立即创建恢复 branch。Reflog 只存在于本地，而且最终会过期；它是安全网，不是备份方案。

---

[← 上一章：变基（Rebase）](09-rebase.md) · [下一章：GitHub 协作流程 →](11-github-workflow.md)
