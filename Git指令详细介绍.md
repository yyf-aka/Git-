# Git指令详细介绍

## 目录
1. [Git简介](#git简介)
2. [Git基础概念](#git基础概念)
3. [Git配置](#git配置)
4. [仓库管理](#仓库管理)
5. [文件操作](#文件操作)
6. [分支管理](#分支管理)
7. [远程仓库](#远程仓库)
8. [版本管理](#版本管理)
9. [合并与变基](#合并与变基)
10. [标签管理](#标签管理)
11. [撤销操作](#撤销操作)
12. [日志与历史](#日志与历史)
13. [高级功能](#高级功能)
14. [Git工作流](#git工作流)
15. [常见问题解决](#常见问题解决)

---

## Git简介

Git是一个分布式版本控制系统，由Linux创始人Linus Torvalds于2005年开发。它被广泛用于软件开发中的源代码管理，具有速度快、设计简单、对非线性开发模式的强力支持等特点。

### Git的优势
- **分布式**：每个工作目录都是完整的代码库
- **快速**：本地操作，速度极快
- **数据完整性**：通过SHA-1哈希值确保数据完整
- **非线性开发**：支持复杂的分支合并
- **轻量级分支**：创建和切换分支成本极低

---

## Git基础概念

### 工作区域
1. **工作目录（Working Directory）**：当前正在工作的目录
2. **暂存区（Staging Area/Index）**：临时存储区域，用于准备下次提交
3. **版本库（Repository）**：Git用来保存项目的元数据和对象数据库

### 文件状态
- **未跟踪（Untracked）**：新文件，尚未被Git管理
- **已修改（Modified）**：文件已修改但未暂存
- **已暂存（Staged）**：文件已暂存，准备提交
- **已提交（Committed）**：文件已安全保存在本地数据库

### 核心对象
- **Blob**：存储文件内容
- **Tree**：存储目录结构
- **Commit**：存储提交信息
- **Tag**：存储标签信息

---

## Git配置

### 全局配置
```bash
# 设置用户信息
git config --global user.name "您的姓名"
git config --global user.email "您的邮箱"

# 设置默认编辑器
git config --global core.editor vim

# 设置默认分支名
git config --global init.defaultBranch main

# 设置行尾符处理
git config --global core.autocrlf true    # Windows
git config --global core.autocrlf input   # Mac/Linux

# 设置别名
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
```

### 查看配置
```bash
# 查看所有配置
git config --list

# 查看特定配置
git config user.name
git config user.email

# 查看配置文件位置
git config --list --show-origin
```

### 配置文件位置
- **系统级**：`/etc/gitconfig`
- **用户级**：`~/.gitconfig` 或 `~/.config/git/config`
- **项目级**：`.git/config`

---

## 仓库管理

### 初始化仓库
```bash
# 在当前目录初始化Git仓库
git init

# 初始化带工作目录的仓库
git init <项目名>

# 初始化裸仓库（用于服务器）
git init --bare
```

### 克隆仓库
```bash
# 克隆远程仓库
git clone <仓库URL>

# 克隆到指定目录
git clone <仓库URL> <目录名>

# 克隆指定分支
git clone -b <分支名> <仓库URL>

# 浅克隆（只克隆最近的提交）
git clone --depth 1 <仓库URL>
```

### 查看仓库状态
```bash
# 查看仓库状态
git status

# 简洁格式显示状态
git status -s

# 显示被忽略的文件
git status --ignored
```

---

## 文件操作

### 添加文件
```bash
# 添加特定文件到暂存区
git add <文件名>

# 添加多个文件
git add <文件1> <文件2>

# 添加所有修改的文件
git add .

# 添加所有文件（包括删除的）
git add -A

# 交互式添加
git add -i

# 添加文件的部分内容
git add -p
```

### 提交更改
```bash
# 提交暂存区的更改
git commit -m "提交信息"

# 添加并提交（跳过暂存区）
git commit -am "提交信息"

# 修改最后一次提交
git commit --amend

# 空提交（用于触发CI等）
git commit --allow-empty -m "空提交"
```

### 删除文件
```bash
# 从工作区和暂存区删除文件
git rm <文件名>

# 只从暂存区删除，保留工作区文件
git rm --cached <文件名>

# 递归删除目录
git rm -r <目录名>

# 强制删除
git rm -f <文件名>
```

### 移动/重命名文件
```bash
# 移动或重命名文件
git mv <原文件名> <新文件名>

# 移动文件到目录
git mv <文件名> <目录名>/
```

### 查看文件差异
```bash
# 查看工作区与暂存区的差异
git diff

# 查看暂存区与最后提交的差异
git diff --cached

# 查看工作区与最后提交的差异
git diff HEAD

# 查看两个提交间的差异
git diff <提交1> <提交2>

# 查看特定文件的差异
git diff <文件名>
```

---

## 分支管理

### 创建和切换分支
```bash
# 查看所有分支
git branch

# 查看远程分支
git branch -r

# 查看所有分支（本地和远程）
git branch -a

# 创建新分支
git branch <分支名>

# 创建并切换到新分支
git checkout -b <分支名>

# 基于特定提交创建分支
git checkout -b <分支名> <提交哈希>

# 切换分支
git checkout <分支名>

# 切换到上一个分支
git checkout -
```

### 分支操作
```bash
# 重命名分支
git branch -m <旧分支名> <新分支名>

# 重命名当前分支
git branch -m <新分支名>

# 删除分支
git branch -d <分支名>

# 强制删除分支
git branch -D <分支名>

# 删除远程分支
git push origin --delete <分支名>
```

### 分支比较
```bash
# 查看分支包含的提交
git branch --contains <提交哈希>

# 查看已合并的分支
git branch --merged

# 查看未合并的分支
git branch --no-merged
```

---

## 远程仓库

### 管理远程仓库
```bash
# 查看远程仓库
git remote

# 查看远程仓库详细信息
git remote -v

# 添加远程仓库
git remote add <远程名> <URL>

# 重命名远程仓库
git remote rename <旧名称> <新名称>

# 删除远程仓库
git remote remove <远程名>

# 修改远程仓库URL
git remote set-url <远程名> <新URL>
```

### 同步远程仓库
```bash
# 获取远程仓库更新（不合并）
git fetch

# 获取特定远程仓库更新
git fetch <远程名>

# 获取特定分支更新
git fetch <远程名> <分支名>

# 拉取并合并远程更新
git pull

# 拉取特定远程分支
git pull <远程名> <分支名>

# 推送到远程仓库
git push

# 推送到特定远程分支
git push <远程名> <分支名>

# 推送所有分支
git push --all

# 推送标签
git push --tags
```

### 跟踪分支
```bash
# 设置上游分支
git branch -u <远程名>/<分支名>

# 查看跟踪关系
git branch -vv

# 推送并设置上游分支
git push -u <远程名> <分支名>
```

---

## 版本管理

### 查看提交历史
```bash
# 查看提交历史
git log

# 简洁格式显示
git log --oneline

# 显示差异
git log -p

# 显示统计信息
git log --stat

# 图形化显示分支
git log --graph

# 自定义格式
git log --pretty=format:"%h - %an, %ar : %s"

# 限制显示数量
git log -n 5

# 按时间范围筛选
git log --since="2 weeks ago"
git log --until="2023-01-01"

# 按作者筛选
git log --author="作者名"

# 按提交信息筛选
git log --grep="关键字"
```

### 查看特定提交
```bash
# 显示特定提交详情
git show <提交哈希>

# 显示特定文件在某次提交的内容
git show <提交哈希>:<文件路径>

# 显示提交涉及的文件
git show --name-only <提交哈希>
```

### 比较版本
```bash
# 比较两个提交
git diff <提交1>..<提交2>

# 比较分支
git diff <分支1>..<分支2>

# 查看分支独有的提交
git log <分支1>..<分支2>
```

---

## 合并与变基

### 合并操作
```bash
# 合并分支
git merge <分支名>

# 快进合并
git merge --ff-only <分支名>

# 禁用快进合并
git merge --no-ff <分支名>

# 压缩合并
git merge --squash <分支名>

# 中止合并
git merge --abort
```

### 变基操作
```bash
# 变基当前分支到目标分支
git rebase <目标分支>

# 交互式变基
git rebase -i <起始提交>

# 继续变基
git rebase --continue

# 跳过冲突的提交
git rebase --skip

# 中止变基
git rebase --abort
```

### 解决冲突
```bash
# 查看冲突文件
git status

# 手动编辑冲突文件后标记为已解决
git add <冲突文件>

# 继续合并/变基
git commit  # 对于合并
git rebase --continue  # 对于变基
```

---

## 标签管理

### 创建标签
```bash
# 创建轻量标签
git tag <标签名>

# 创建带注释的标签
git tag -a <标签名> -m "标签说明"

# 为特定提交创建标签
git tag -a <标签名> <提交哈希> -m "标签说明"

# 使用GPG签名标签
git tag -s <标签名> -m "标签说明"
```

### 查看标签
```bash
# 列出所有标签
git tag

# 按模式查找标签
git tag -l "v1.8.5*"

# 查看标签详情
git show <标签名>
```

### 删除标签
```bash
# 删除本地标签
git tag -d <标签名>

# 删除远程标签
git push origin :refs/tags/<标签名>
git push origin --delete <标签名>
```

### 推送标签
```bash
# 推送单个标签
git push origin <标签名>

# 推送所有标签
git push origin --tags

# 推送带注释的标签
git push origin --follow-tags
```

---

## 撤销操作

### 撤销工作区更改
```bash
# 撤销文件的修改
git checkout -- <文件名>

# 撤销所有修改
git checkout -- .

# 使用restore命令（Git 2.23+）
git restore <文件名>
git restore .
```

### 撤销暂存区更改
```bash
# 取消暂存文件
git reset HEAD <文件名>

# 取消所有暂存
git reset HEAD

# 使用restore命令
git restore --staged <文件名>
```

### 撤销提交
```bash
# 撤销最后一次提交（保留更改）
git reset --soft HEAD~1

# 撤销最后一次提交（撤销暂存）
git reset HEAD~1

# 撤销最后一次提交（完全撤销）
git reset --hard HEAD~1

# 撤销到特定提交
git reset --hard <提交哈希>

# 创建反向提交
git revert <提交哈希>
```

### 清理操作
```bash
# 删除未跟踪的文件
git clean -f

# 删除未跟踪的文件和目录
git clean -fd

# 删除被忽略的文件
git clean -fX

# 删除所有未跟踪和被忽略的文件
git clean -fx

# 预览将要删除的文件
git clean -n
```

---

## 日志与历史

### 查看引用日志
```bash
# 查看引用日志
git reflog

# 查看特定分支的引用日志
git reflog <分支名>

# 查看指定时间内的引用日志
git reflog --since="2 hours ago"
```

### 查找提交
```bash
# 按提交信息搜索
git log --grep="搜索关键字"

# 按文件内容搜索
git log -S "搜索内容"

# 按正则表达式搜索
git log --grep="正则表达式" --extended-regexp

# 查找引入或删除某行的提交
git log -L <起始行>,<结束行>:<文件名>
```

### 责任追踪
```bash
# 查看文件每一行的最后修改者
git blame <文件名>

# 查看特定行范围
git blame -L <起始行>,<结束行> <文件名>

# 查看文件在特定提交时的责任信息
git blame <提交哈希> -- <文件名>
```

---

## 高级功能

### 储藏（Stash）
```bash
# 储藏当前工作
git stash

# 储藏时添加说明
git stash save "储藏说明"

# 储藏包括未跟踪的文件
git stash -u

# 查看储藏列表
git stash list

# 应用最新的储藏
git stash apply

# 应用特定的储藏
git stash apply stash@{2}

# 应用并删除储藏
git stash pop

# 删除特定储藏
git stash drop stash@{2}

# 清空所有储藏
git stash clear
```

### 子模块（Submodule）
```bash
# 添加子模块
git submodule add <仓库URL> <路径>

# 初始化子模块
git submodule init

# 更新子模块
git submodule update

# 初始化并更新所有子模块
git submodule update --init --recursive

# 拉取子模块最新代码
git submodule update --remote

# 删除子模块
git submodule deinit <子模块名>
git rm <子模块路径>
```

### 工作树（Worktree）
```bash
# 添加工作树
git worktree add <路径> <分支名>

# 列出所有工作树
git worktree list

# 删除工作树
git worktree remove <路径>

# 清理工作树
git worktree prune
```

### 二分查找（Bisect）
```bash
# 开始二分查找
git bisect start

# 标记当前提交为坏的
git bisect bad

# 标记特定提交为好的
git bisect good <提交哈希>

# 继续查找过程
git bisect good  # 或 git bisect bad

# 结束二分查找
git bisect reset
```

### Cherry-pick
```bash
# 应用特定提交到当前分支
git cherry-pick <提交哈希>

# 应用多个提交
git cherry-pick <提交1> <提交2>

# 应用提交范围
git cherry-pick <起始提交>..<结束提交>

# 只应用更改不提交
git cherry-pick -n <提交哈希>
```

---

## Git工作流

### Git Flow
Git Flow是一种基于Git的分支管理策略：

```bash
# 主分支
- main/master: 生产环境代码
- develop: 开发环境代码

# 辅助分支
- feature/*: 功能开发分支
- release/*: 发布准备分支
- hotfix/*: 紧急修复分支
```

### GitHub Flow
简化的工作流程：
1. 从main分支创建功能分支
2. 在功能分支上开发
3. 创建Pull Request
4. 代码审查
5. 合并到main分支

### GitLab Flow
结合环境分支的工作流：
```bash
main → pre-production → production
```

---

## 常见问题解决

### 1. 合并冲突
```bash
# 查看冲突文件
git status

# 手动解决冲突后
git add <冲突文件>
git commit
```

### 2. 误删分支恢复
```bash
# 查找被删除的分支
git reflog

# 恢复分支
git checkout -b <分支名> <提交哈希>
```

### 3. 修改提交历史
```bash
# 交互式变基修改历史
git rebase -i HEAD~3

# 修改最后一次提交信息
git commit --amend
```

### 4. 大文件处理
```bash
# 使用Git LFS处理大文件
git lfs track "*.zip"
git add .gitattributes
git add 大文件.zip
git commit -m "添加大文件"
```

### 5. 忽略文件权限变更
```bash
git config core.fileMode false
```

### 6. 中文文件名显示问题
```bash
git config --global core.quotepath false
```

### 7. 换行符问题
```bash
# Windows
git config --global core.autocrlf true

# Mac/Linux
git config --global core.autocrlf input
```

---

## 常用Git别名

```bash
# 配置常用别名
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.dt difftool
git config --global alias.mt mergetool
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
git config --global alias.unstage 'reset HEAD --'
git config --global alias.tree 'log --graph --pretty=format:"%h -%d %s (%cr) <%an>" --abbrev-commit'
```

---

## 总结

Git是一个功能强大的版本控制系统，掌握其基本操作对于软件开发至关重要。本文档涵盖了从基础配置到高级功能的各个方面。建议：

1. **从基础开始**：先熟练掌握基本的add、commit、push、pull操作
2. **理解概念**：深入理解工作区、暂存区、版本库的概念
3. **实践练习**：通过实际项目练习各种Git操作
4. **学习工作流**：根据团队需要选择合适的Git工作流
5. **持续学习**：Git功能丰富，需要不断学习和实践

记住：Git的学习是一个渐进的过程，不要试图一次性掌握所有功能。先掌握核心功能，再逐步学习高级特性。 