# 练习 2：分支管理

## 任务清单

### 步骤 1：查看当前分支
```bash
git branch
```
你会看到 * 在 main（或 master）前面，表示当前分支。

### 步骤 2：创建新分支
```bash
git branch feature-exercise
```

### 步骤 3：切换到新分支
```bash
git checkout feature-exercise
# 或
git switch feature-exercise
```

### 步骤 4：在新分支上修改文件
```bash
# 在 exercises/02-branching.md 文件末尾添加一行
echo "## 我的分支练习" >> exercises/02-branching.md

# 查看修改
git diff

# 提交修改
git add .
git commit -m "在 feature-exercise 分支添加内容"
```

### 步骤 5：切换回主分支
```bash
git switch main
```

### 步骤 6：查看文件内容
```bash
cat exercises/02-branching.md
```
你会发现刚才添加的内容不见了！因为你在 main 分支。

### 步骤 7：合并分支
```bash
git merge feature-exercise
```

### 步骤 8：删除已合并的分支
```bash
git branch -d feature-exercise
```

---

## ✅ 完成标志

- 成功创建并切换到 feature-exercise 分支
- 在分支上做了提交
- 成功合并回 main
- 删除了 feature 分支

## 🌟 挑战任务

1. 创建两个分支：feature-a 和 feature-b
2. 在每个分支上做不同的修改
3. 尝试按不同顺序合并，观察结果
4. 使用 `git log --graph --oneline --all` 查看分支图
