# 参与贡献

欢迎修正错误、澄清解释、改进示例，以及提出目标明确的问题。对于一本精简手册，小贡献尤其有价值。

## 报告错误或不清楚的解释

创建 GitHub Issue，并尽量包含：

- 对应页面与小节。
- 错误或不清楚之处。
- 你原本希望理解什么。
- 如果涉及技术准确性，附上资料来源或测试过的示例。

请先搜索已有 Issues。无需先写出完美答案；准确指出读者在哪里产生困惑，本身就很有价值。

## 提议内容改进

需要讨论的改动，请先创建 Issue。错别字、失效链接、经过验证的修正或小型表达改进，可以直接提交目标明确的 Pull Request。

对于较大的修改，请先描述读者面对的问题，再开始撰写大段替代内容。除非项目已经达成共识，否则请保持 12 章顺序与「心智模型优先」的写法。

## 提交 Pull Request

如果不能直接向本仓库推送 branch，请先在 GitHub 上 fork，然后执行：

```bash
git clone https://github.com/YOU/git-you-need-to-know.git
cd git-you-need-to-know
git switch -c docs/short-description
```

完成一个目标明确的改进。检查并提交：

```bash
git diff
git add <changed-paths>
git diff --staged
git commit -m "澄清某个概念"
git push -u origin docs/short-description
```

创建 Pull Request，说明读者遇到的问题、你的解决方案和执行过的检查。收到 review 意见后，可以在同一 branch 上继续提交 commits。

第一次使用这套流程？请阅读 [GitHub 协作流程](docs/11-github-workflow.md)。

## 写作约定

- 开头先给出核心概念。
- 使用短句、短段落和一致的 Git 术语。
- 解释命令改变了什么，而不只展示语法。
- 优先提供一个最小、可运行的示例，不堆砌命令。
- 只有在关系更清楚时才使用图表。
- 明确标记破坏性操作或历史重写操作。
- 链接前置知识与下一步内容。
- 在合适的情况下，与 `field-notes` 示例仓库保持一致。

## 提交前检查

- 在窄屏和桌面端阅读渲染后的 Markdown。
- 涉及命令行为时，在一次性仓库中运行示例。
- 检查相对链接和标题名称。
- 确认图表在 GitHub 的纯文本环境中仍然清晰。
- 搜索冲突标记：`git grep -n '<<<<<<<'`。
- 用 `git diff --check` 检查空白字符错误。
- 检查 `git status`，确保 Pull Request 只包含有意修改的文件。

不要在包含重要工作的仓库中测试破坏性命令。

你的贡献会帮助这本手册保持准确、精简，并继续服务下一位读者。

---

[返回 README](README.md)
