# 1. 心智模型

- 一句话概括，Git 是一个分布式版本控制系统（Distributed Version Control System）。

- Git = 代码世界里的“存档系统”。

- Git 记录的是**项目在不同时间点的快照**。大多数日常操作，都是让改动在四个位置之间流动。

```text
工作区（Working Tree） → 暂存区（Staging Area） → 本地仓库（Local Repository） → 远程仓库（Remote Repository）
          编辑                git add                 git commit                    git push
```

## 四个位置

| 位置 | 保存什么 | 回答什么问题 |
| --- | --- | --- |
| 工作区 | 你能看见和编辑的文件 | 我现在正在改什么？ |
| 暂存区 | 为下一次 commit 精确选中的改动 | 我下一次准备记录什么？ |
| 本地仓库 | 保存在你电脑 `.git` 中的 commits | 我已经记录了什么？ |
| 远程仓库 | GitHub 等服务器上供团队共享的 commits | 团队已经发布了什么？ |

同一个文件在这四个位置中可以有不同版本。这很正常。Git 命令做的事情，本质上就是比较这些位置，或在它们之间移动信息。

## 一次改动的完整旅程

```bash
printf '# 田野笔记\n' > README.md       # 编辑工作区
git add README.md                       # 把改动复制到暂存区
git commit -m "添加项目标题"             # 在本地永久记录一个快照
git push                                # 把 commits 发布到远程仓库
```

执行 `git add` 后，如果再次编辑 `README.md`，暂存区中的副本不会自动更新。如果新改动也属于这次 commit，需要再次执行 `git add README.md`。

## Git 通常存储快照

可以把每个 commit 理解成「快照 + 元数据」：

```text
commit C  →  快照 C + 作者 + 时间 + 消息 + 父 commit B
commit B  →  快照 B + 作者 + 时间 + 消息 + 父 commit A
commit A  →  第一个快照
```

Git 可以展示两个快照之间的 diff，但一个 commit 并不只是一包被修改的行。理解这个区别，会让 branch、merge 和恢复操作更容易掌握。

## 你的导航仪

经常运行：

```bash
git status
```

它会报告当前 branch，以及工作区、暂存区和当前 commit 之间的差异。执行陌生命令前后，都值得看一眼。

> **核心原则：**弄清一个命令从哪里读取，又会改变哪里。

---

[下一章：仓库 →](02-repository.md)
