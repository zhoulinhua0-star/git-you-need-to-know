# 3. 工作区与暂存区

工作区是你编辑文件的地方。暂存区（Staging Area，也叫 **index**）是你组装下一次 commit 的地方。

```text
当前 commit（HEAD） → 工作区改动 → 暂存区中的选择
                           git add ─────────→
```

## 查看每一种差异

```bash
git status               # 汇总已暂存、未暂存和未跟踪的文件
git diff                 # 比较工作区与暂存区
git diff --staged        # 比较暂存区与当前 commit
```

假设 `notes.md` 中有两处无关的修改，而你只想暂存文档修正：

```bash
git add -p notes.md
```

Git 会逐个显示改动片段（**hunk**）。输入 `y` 暂存当前片段，输入 `n` 跳过；条件允许时可输入 `s` 继续拆分。

如果一个文件中的全部改动都属于同一件事，可以按路径整体暂存：

```bash
git add README.md notes.md
```

## 发生了什么？

`git add` 把选中的文件内容复制到 index。它不会创建永久历史记录；`git commit` 才会。

如果暂存了错误的文件，可以把它移出下一次 commit，同时保留工作区中的修改：

```bash
git restore --staged notes.md
```

> **常见错误：**`git add .` 很方便，但也可能暂存生成文件、密钥或无关改动。Commit 前先检查 `git status` 和 `git diff --staged`。

用 `.gitignore` 排除仓库永远不应跟踪的内容，例如本地构建产物。把一个已经被跟踪的文件加入 `.gitignore`，并不会让 Git 停止跟踪它。

---

[← 上一章：仓库](02-repository.md) · [下一章：提交（Commit）→](04-commit.md)
