# 🎓 Git 和 GitHub 交互式教学项目

> 欢迎来到你的第一个 Git/GitHub 教学项目！这个项目专为你设计，通过实际操作来学习 Git 和 GitHub。

## 📋 目录

- [项目简介](#项目简介)
- [前置知识](#前置知识)
- [第一课：Git 基础](#第一课git-基础)
- [第二课：GitHub 远程仓库](#第二课github-远程仓库)
- [第三课：分支管理](#第三课分支管理)
- [第四课：协作开发](#第四课协作开发)
- [常用命令速查](#常用命令速查)
- [实战练习](#实战练习)

---

## 项目简介

这个项目本身就是学习材料！你将在这个项目中练习所有 Git 操作，最后把它推送到你的 GitHub 上。

### 你会学到：

✅ Git 的核心概念（工作区、暂存区、仓库）
✅ 基本命令：add, commit, push, pull
✅ 分支管理
✅ 处理冲突
✅ GitHub 的使用
✅ Pull Request 流程

---

## 前置知识

### 什么是 Git？

**Git** 是一个分布式版本控制系统，用于跟踪文件变化和协同工作。

### 什么是 GitHub？

**GitHub** 是一个基于 Git 的代码托管平台，提供远程仓库、协作工具等功能。

### 核心概念图解：

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   工作区    │ ──▶ │   暂存区    │ ──▶ │   本地仓库  │
│ (Working    │ add │   (Staging  │commit│ (Repository)│
│  Directory) │     │    Area)    │     │             │
└─────────────┘     └─────────────┘     └─────────────┘
                                               │
                                               │ push
                                               ▼
                                         ┌─────────────┐
                                         │  远程仓库   │
                                         │  (GitHub)   │
                                         └─────────────┘
```

---

## 第一课：Git 基础

### 1.1 初始化仓库

在你项目的根目录下运行：

```bash
git init
```

这个命令会创建一个 `.git` 隐藏文件夹，Git 在这里存储所有版本信息。

### 1.2 配置用户信息

**首次使用必须配置！**

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

💡 **提示**：这个邮箱应该和你的 GitHub 账号邮箱一致。

### 1.3 查看状态

```bash
git status
```

这是你**最常用的命令**！它会告诉你：
- 哪些文件被修改了
- 哪些文件在暂存区
- 当前在哪个分支

### 1.4 添加文件到暂存区

```bash
# 添加单个文件
git add README.md

# 添加所有文件
git add .

# 添加特定类型文件
git add *.txt
```

### 1.5 提交更改

```bash
git commit -m "添加第一次提交"
```

💡 **提交信息规范**：
- ✅ 好的：`"添加用户登录功能"`
- ❌ 不好的：`"更新文件"`、`"fix"`

### 1.6 查看提交历史

```bash
# 简洁版
git log --oneline

# 详细版
git log

# 图形化（查看分支）
git log --graph --oneline
```

---

## 第二课：GitHub 远程仓库

### 2.1 在 GitHub 创建仓库

1. 登录 [GitHub](https://github.com)
2. 点击右上角 `+` → `New repository`
3. 填写仓库名称（例如：`git-learning-journey`）
4. 选择 Public 或 Private
5. **不要**勾选 "Initialize this repository with a README"
6. 点击 `Create repository`

### 2.2 连接远程仓库

创建后，GitHub 会显示连接命令。选择你需要的：

```bash
# SSH 方式（推荐，需要配置 SSH 密钥）
git remote add origin git@github.com:你的用户名/仓库名.git

# HTTPS 方式
git remote add origin https://github.com/你的用户名/仓库名.git
```

### 2.3 推送到 GitHub

```bash
# 第一次推送（设置上游分支）
git push -u origin main

# 之后推送
git push
```

💡 **注意**：Git 默认分支叫 `main`，旧版本可能是 `master`。

### 2.4 查看远程仓库

```bash
# 查看远程仓库列表
git remote -v

# 查看远程仓库详细信息
git remote show origin
```

---

## 第三课：分支管理

### 3.1 为什么需要分支？

分支让你可以：
- 🧪 实验新功能而不影响主线
- 🐛 修复 bug 时保持代码稳定
- 👥 多人同时开发不同功能

```
          main (稳定版本)
           │
           ├─── feature-A (开发功能 A)
           │
           └─── bugfix-123 (修复 bug #123)
```

### 3.2 分支基本操作

```bash
# 查看所有分支
git branch

# 创建新分支
git branch feature-login

# 切换到分支
git checkout feature-login

# 创建并切换（常用！）
git checkout -b feature-login

# 或者使用新命令（更直观）
git switch feature-login        # 切换分支
git switch -c feature-login     # 创建并切换
```

### 3.3 合并分支

```bash
# 1. 切换回主分支
git switch main

# 2. 合并 feature 分支
git merge feature-login

# 3. 删除已合并的分支
git branch -d feature-login
```

### 3.4 处理合并冲突

当两个人修改同一文件的同一行时，会产生冲突：

```
<<<<<<< HEAD
当前分支的内容
=======
要合并分支的内容
>>>>>>> feature-login
```

**解决步骤**：
1. 打开冲突文件
2. 编辑文件，保留需要的代码，删除冲突标记
3. `git add 冲突文件`
4. `git commit`（不需要加信息，会自动生成）

---

## 第四课：协作开发

### 4.1 Pull Request (PR) 流程

**这是 GitHub 协作的核心！**

```
1. 从 main 创建分支 ──▶ feature-branch
                         │
2. 在分支上开发并提交 ────▤
                         │
3. 推送到 GitHub ────────▤
                         │
4. 创建 Pull Request ────▤
                         │
5. 代码审查 ─────────────▤
                         │
6. 合并到 main ──────────▘
```

### 4.2 创建 Pull Request

1. 在 GitHub 上打开你的仓库
2. 点击 `Pull requests` → `New pull request`
3. 选择要合并的分支
4. 填写标题和描述
5. 点击 `Create pull request`

### 4.3 从远程仓库获取更新

```bash
# 获取远程更新但不合并
git fetch origin

# 获取并合并（常用）
git pull origin main

# 等同于
git fetch origin
git merge origin/main
```

---

## 常用命令速查

### 每日必备

| 命令 | 作用 |
|------|------|
| `git status` | 查看当前状态 |
| `git add .` | 添加所有修改 |
| `git commit -m "信息"` | 提交 |
| `git push` | 推送到远程 |

### 查看和比较

| 命令 | 作用 |
|------|------|
| `git log --oneline` | 简洁历史 |
| `git diff` | 查看未暂存的修改 |
| `git diff --staged` | 查看已暂存的修改 |
| `git show` | 查看最后一次提交 |

### 撤销操作

| 命令 | 作用 |
|------|------|
| `git checkout -- 文件` | 撤销工作区修改 |
| `git restore 文件` | 新版撤销命令 |
| `git reset HEAD 文件` | 取消暂存 |
| `git commit --amend` | 修改最后一次提交 |

### 分支操作

| 命令 | 作用 |
|------|------|
| `git branch` | 查看分支 |
| `git switch -c 新分支` | 创建并切换 |
| `git merge 分支` | 合并分支 |
| `git branch -d 分支` | 删除分支 |

---

## 实战练习

### 🎯 练习 1：基础工作流

```bash
# 1. 初始化
git init
git config user.name "你的名字"
git config user.email "你的邮箱"

# 2. 创建并提交
echo "# 我的第一个项目" > README.md
git add README.md
git commit -m "初始提交：添加 README"

# 3. 修改并提交
echo "## 项目简介" >> README.md
echo "这是我的学习项目" >> README.md
git add README.md
git commit -m "添加项目简介"

# 4. 查看历史
git log --oneline
```

### 🎯 练习 2：分支练习

```bash
# 1. 创建并切换到新分支
git switch -c add-examples

# 2. 在分支上工作
echo "# 示例文件" > examples.md
git add examples.md
git commit -m "添加示例文件"

# 3. 切回主分支
git switch main

# 4. 合并
git merge add-examples

# 5. 清理
git branch -d add-examples
```

### 🎯 练习 3：推送到 GitHub

```bash
# 1. 在 GitHub 创建仓库（名为 git-learning）

# 2. 连接远程仓库
git remote add origin https://github.com/你的用户名/git-learning.git

# 3. 推送
git push -u origin main

# 4. 在 GitHub 网页上查看！
```

---

## 🎓 学习建议

1. **边学边练**：不要只看，一定要动手操作
2. **犯错没关系**：Git 的设计允许你撤销大部分操作
3. **建立肌肉记忆**：多用才能记住
4. **查看帮助**：`git 命令 --help` 或 `git help 命令`

## 📚 推荐资源

- [Git 官方文档](https://git-scm.com/doc)
- [GitHub 官方教程](https://docs.github.com/zh/get-started)
- [GitHub Skills](https://skills.github.com/) - 交互式学习

## 💡 下一步

完成这个项目后，你可以：

1. 把这个项目推送到 GitHub
2. 在 GitHub 上编辑 README
3. 尝试创建 Pull Request
4. 探索 GitHub Actions、Issues 等功能

---

**记住**：最好的学习方式就是实际使用！现在就开始吧！🚀
- [练习 4：综合实战](exercises/04-advanced.md)
