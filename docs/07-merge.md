# 7. 合并（Merge）

Merge 会组合不同开发线上的工作，同时保留它们曾经分叉的事实。

## 快进合并（Fast-forward Merge）

如果 topic branch 创建后，`main` 没有新增 commit，Git 只需移动 branch 名字：

```text
合并前：A──B  ← main
             └──C──D  ← docs/staging

合并后：A──B──C──D  ← main
```

```bash
git switch main
git merge --ff-only docs/staging
```

这里不需要 merge commit。

## 三方合并（Three-way Merge）

如果两个 branches 都有新 commits，Git 会把两个 branch 的顶端与共同祖先进行比较，然后创建一个有两个父 commits 的新 commit：

```text
      C──D  ← docs/staging
     /    \
A──B──E────M  ← main
```

```bash
git switch main
git merge docs/staging
```

如果 Git 能自动组合改动，就会创建 `M`。如果无法安全组合相互竞争的修改，merge 会暂停，等待你解决冲突。

## 什么时候适合 merge

当 branch 结构本身有意义，或需要保留已经公开的历史时，merge 很合适。它不会重写被合并的 commits。

合并前先检查：

```bash
git status
git log --oneline --graph --decorate --all
```

最好从干净的工作区开始。如果想取消一次发生冲突的 merge，并返回合并前的状态：

```bash
git merge --abort
```

> `git merge --abort` 只用于正在进行的 merge，不是通用撤销命令。

---

[← 上一章：远程仓库（Remote）](06-remote.md) · [下一章：冲突（Conflict）→](08-conflict.md)
