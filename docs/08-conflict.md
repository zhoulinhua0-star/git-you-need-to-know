# 8. 冲突（Conflict）

冲突表示 Git 需要人来做决定。这是一次正常暂停，不代表仓库损坏了。

当两个 branches 修改了相互重叠的行，或一边删除文件、另一边继续编辑时，经常会发生冲突。

## 一套可重复的解决流程

1. 查看哪些内容尚未解决。

   ```bash
   git status
   ```

2. 打开每个冲突文件。Git 会标出相互竞争的内容：

   ```text
   <<<<<<< HEAD
   先阅读暂存区章节。
   =======
   从心智模型开始阅读。
   >>>>>>> docs/navigation
   ```

3. 把文件编辑成正确的最终内容，并删除所有标记行。

4. 标记冲突已解决，然后检查结果。

   ```bash
   git add README.md
   git diff --staged
   git status
   ```

5. 完成当前操作。

   ```bash
   git commit              # merge
   git rebase --continue   # rebase
   ```

你要解决的是内容含义，而不只是删除标记。正确结果可能组合双方，也可能双方都不用。

## 安全退出

使用与当前操作对应的 abort 命令：

```bash
git merge --abort
git rebase --abort
git cherry-pick --abort
```

Git 会尝试回到该操作开始前的状态。

> **不要提交冲突标记。**完成前搜索一次：`git grep -n '<<<<<<<'`。

保持 branch 目标单一、commit 小而完整、经常同步，并避免把无关的格式调整与功能修改混在一起，都能减少冲突。

---

[← 上一章：合并（Merge）](07-merge.md) · [下一章：变基（Rebase）→](09-rebase.md)
