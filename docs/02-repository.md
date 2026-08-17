# 2. 仓库

Git 仓库是一个项目，加上用于保存历史与引用的 `.git` 目录。

```text
field-notes/
├── .git/       ← Git 的数据库和配置
├── README.md   ← 工作区中的文件
└── notes.md
```

删除 `.git` 不会删除项目文件，但会移除这个本地仓库的 Git 历史与配置。

## 创建或复制仓库

在现有目录中开始记录历史：

```bash
mkdir field-notes
cd field-notes
git init
```

或者复制一个已有仓库及其历史：

```bash
git clone https://github.com/OWNER/field-notes.git
cd field-notes
```

`git init` 创建 `.git`。`git clone` 会创建目录、下载仓库、检出工作区，并配置一个名为 `origin` 的 remote。

## Git 保存什么

在实用层面，Git 的对象数据库包含：

| 对象 | 作用 |
| --- | --- |
| Blob | 文件内容 |
| Tree | 目录名称，以及指向 blob 或其他 tree 的链接 |
| Commit | 一个 tree、父 commit、作者信息和提交消息 |
| Tag | 可选的具名注释，指向另一个对象 |

对象由根据其内容生成的 hash 标识。Branch 则为 commit hash 提供了便于人类理解的名字。

通常不需要直接编辑 `.git`，请通过 Git 检查仓库：

```bash
git status
git log --oneline
git rev-parse --show-toplevel
```

最后一个命令会输出仓库根目录。在很深的子目录中工作时，它尤其有用。

> **边界：**这个对象模型足以支持日常工作。打包、压缩和底层 plumbing 命令，等需要诊断 Git 内部机制时再了解即可。

---

[← 上一章：心智模型](01-mental-model.md) · [下一章：工作区与暂存区 →](03-staging-area.md)
