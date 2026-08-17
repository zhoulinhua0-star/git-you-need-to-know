# 12. Git 进阶

进阶工具用于解决特定问题。应该按使用意图学习，而不是背一张更长的命令表。

## 暂时收起未完成工作：stash

```bash
git stash push -m "WIP：暂存区示例"
git stash list
git stash pop
```

Stash 会保存已跟踪文件的改动，并从工作区移除它们。要包含未跟踪文件，需要加 `-u`。如果一项工作值得拥有持久历史，优先在私人 branch 上创建普通 commit。

## 复制一个 commit：cherry-pick

```bash
git cherry-pick a1b2c3d
```

Cherry-pick 会把某个 commit 的改动应用到当前 branch，并创建一个新 commit。新 commit 拥有不同的 hash。它适合提取一个特定修复，不应替代正常的 branch 整合。

## 标记一个版本：tag

```bash
git tag -a v1.0.0 -m "第一版"
git push origin v1.0.0
```

Annotated tag 会给某个特定对象一个稳定的名字，通常用于标记发布 commit。Tag 不会像 branch 一样移动。

## 找到第一个出错的 commit：bisect

```bash
git bisect start
git bisect bad
git bisect good v1.0.0
# 测试 Git 检出的版本；重复标记 good 或 bad，直到定位问题
git bisect reset
```

Bisect 会在历史中进行二分查找。可靠的测试能让这个过程既快速又客观。

## 同时检出另一个 branch：worktree

```bash
git worktree add ../field-notes-fix -b fix/navigation main
git worktree list
```

Worktree 让一个仓库拥有多个工作目录。每个关联 worktree 检出不同的 branch，适合在不 stash 当前工作的情况下进行 review 或处理紧急修复。

## 自动执行本地检查：hooks

Hooks 是 `.git/hooks` 中的可执行脚本，例如 `pre-commit`。它们可以格式化文件，或拒绝某个本地操作。

默认情况下，`.git/hooks` 中的 hooks 不会随 clone 分发。如果项目依赖 hooks，应把源文件放在被跟踪的目录中，并说明如何安装或调用。因为本地 hooks 可以被跳过，服务器端检查仍然必不可少。

## 检查模型底层

```bash
git cat-file -t HEAD
git cat-file -p HEAD
git ls-tree HEAD
```

这些 plumbing 命令会展示[仓库](02-repository.md)一章介绍的 commit 与 tree 对象。它们适合学习和诊断；日常工作应优先使用更高层的命令。

> 使用进阶工具前，先检查 `git status`，明确哪些引用或文件会移动，并想好恢复路径。

---

[← 上一章：GitHub 协作流程](11-github-workflow.md) · [返回 README](../README.md) · [打开 Git 速查表](../cheatsheet.md)
