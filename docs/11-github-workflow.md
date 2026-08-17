# 11. GitHub 协作流程

一次 GitHub 贡献，会让一个目标明确的改动从你的 branch 出发，经过审查，最终进入项目的主 branch。

```text
fork → clone → branch → 编辑 → 暂存 → commit → push → Pull Request → review → merge
```

## 完整流程

1. 如果没有权限直接向项目推送 branch，先在 GitHub 上 **Fork** 仓库。Fork 是你在服务器端的副本。

2. **Clone** 你的 fork。

   ```bash
   git clone https://github.com/YOU/git-you-need-to-know.git
   cd git-you-need-to-know
   ```

3. **连接源仓库**，以便获取上游更新。

   ```bash
   git remote add upstream https://github.com/OWNER/git-you-need-to-know.git
   git remote -v
   ```

4. **创建一个目标明确的 branch。**

   ```bash
   git switch -c docs/clarify-staging
   ```

5. **编辑、检查、暂存并提交。**

   ```bash
   git diff
   git add docs/03-staging-area.md
   git diff --staged
   git commit -m "说明如何暂存部分改动"
   ```

6. **把 branch 推送到自己的 fork。**

   ```bash
   git push -u origin docs/clarify-staging
   ```

7. 从你的 branch 向源仓库的 `main` branch 创建 **Pull Request**。说明问题、改动和检查方式。

8. 根据 **review** 意见，在同一 branch 上继续提交 commits。它们会自动出现在 Pull Request 中。

9. 审查通过且自动检查成功后执行 **merge**。项目可能选择 merge commit、squash merge 或 rebase merge。

## 让 branch 保持最新

```bash
git fetch upstream
git switch main
git merge --ff-only upstream/main
git push origin main
```

然后按照项目约定，把更新后的 `main` merge 或 rebase 到你的 topic branch。

本手册会把自己的 Issues、branches、commits 和 Pull Requests 当作学习材料。从一个小修正开始；精确改好一行文字，也是真实的开源贡献。

---

[← 上一章：撤销与恢复](10-undo.md) · [下一章：Git 进阶 →](12-advanced.md)
