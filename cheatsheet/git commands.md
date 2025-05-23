---
tags:
  - commands
  - "#git"
  - cheatsheet
---

## git用户认证

```bash
git config --global credential.helper store
git config --global user.name "jieyinggong"
git config --global user.email "gongjieying0312@gmail.com"
```

## git initialization

```bash
cd my-project
git init

git add .                     # 添加所有文件
git commit -m "Initial commit"

git remote add origin https://github.com/your-username/your-repo.git

git branch -M main           # 重命名当前分支为 main
git push -u origin main
```

## 远程仓库
```bash
git clone https://github.com/username/repo.git

git remote -v                     # 查看远程地址
git remote add origin <url>       # 添加远程仓库
git push -u origin main           # 第一次推送并设置跟踪主分支
```

## 编辑和提交代码
```bash
git add <file>              # 添加文件到暂存区
git add .                   # 添加当前目录所有更改
git commit -m "commit information"    # 提交到本地仓库
```

## push and pull
```bash
git push origin main       # 推送到远程主分支（main）
git pull origin main       # 从远程拉取更新
```

## branch
```bash
git branch                 # 查看所有分支
git branch new-branch      # 创建新分支
git checkout new-branch    # 切换到新分支
git switch -c new-branch   # 创建并切换到新分支（推荐语法）
git merge new-branch       # 合并分支
```

## 撤销和恢复
```bash
git checkout -- <file>             # 撤销对文件的修改
git restore <file>                 # 推荐的撤销方式（新语法）
git reset HEAD <file>             # 取消暂存（从 staging 区恢复到 working 区）
git revert <commit-hash>          # 撤销某次提交（生成新的反向提交）
```
