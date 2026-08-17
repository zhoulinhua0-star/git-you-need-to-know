# 你需要知道的 Git

> 一本极简、实用的 Git 手册，帮你建立正确的心智模型，并自信地使用 Git。

理解 Git 中「什么发生了移动」，Git 就会简单得多。本书先解释模型，再介绍操作这个模型的命令。适合开发者、学生，以及只偶尔使用 Git、希望快速查阅而不想面对命令堆砌的读者。

```text
工作区（Working Tree） → 暂存区（Staging Area） → 本地仓库（Local Repository） → 远程仓库（Remote Repository）
          编辑                    暂存                    提交                         推送
```

建议从 **[心智模型](docs/01-mental-model.md)** 开始。Git 新手可以按顺序阅读；遇到具体问题时，也可以直接跳到对应章节。

## 章节目录

1. [心智模型](docs/01-mental-model.md)
2. [仓库](docs/02-repository.md)
3. [工作区与暂存区](docs/03-staging-area.md)
4. [提交（Commit）](docs/04-commit.md)
5. [分支（Branch）](docs/05-branch.md)
6. [远程仓库（Remote）](docs/06-remote.md)
7. [合并（Merge）](docs/07-merge.md)
8. [冲突（Conflict）](docs/08-conflict.md)
9. [变基（Rebase）](docs/09-rebase.md)
10. [撤销与恢复](docs/10-undo.md)
11. [GitHub 协作流程](docs/11-github-workflow.md)
12. [Git 进阶](docs/12-advanced.md)

只想马上找到命令？打开按意图组织的 **[Git 速查表](cheatsheet.md)**。

看不懂 `-c`、`-m`、`-u` 这类写法？阅读 **[Git 命令行选项科普](git-command-options.md)**，了解短选项、长选项、参数与常见用法。

## 在开放协作中学习

这个仓库本身也是练习 Git 的地方。你可以修正错别字、改进示例、创建 Issue，或提交 Pull Request。[贡献指南](CONTRIBUTING.md)会带你走完整个流程。

这本手册会随着 Git 的发展和我们理解的深入持续更新。
