# Git 命令速查

## 0. 先记住 Git 的整体流程

```text
工作区
  │
  │ git add
  ↓
暂存区
  │
  │ git commit
  ↓
本地仓库
  │
  │ git push
  ↓
远程仓库（GitHub）
```

同时，本地仓库中可以有多个分支：

```text
main
dev
feature-login
fix-bug
```

---

# 1. 查看当前状态

## `git status`

```bash
git status
```

作用：

查看当前 Git 仓库的状态，包括：

* 当前在哪个分支
* 哪些文件被修改
* 哪些文件已经进入暂存区
* 哪些文件还没有 `git add`
* 有没有未跟踪文件

示例：

```bash
git status
```

输出可能类似：

```text
On branch main

Changes not staged for commit:
    modified: main.py

Untracked files:
    test.py
```

这是 Git 中最常用的命令之一。

建议：

```text
不知道现在发生了什么 → 先 git status
```

---

# 2. 初始化 Git 仓库

## `git init`

```bash
git init
```

作用：

将当前文件夹初始化为 Git 仓库。

执行后会生成：

```text
.git/
```

这个 `.git` 文件夹保存 Git 的版本历史、分支、提交等信息。

例如：

```bash
cd my-project
git init
```

适用于：

```text
你已经有一个本地项目
↓
现在想开始使用 Git 管理它
```

---

# 3. 克隆 GitHub 项目

## `git clone`

```bash
git clone <仓库地址>
```

例如：

```bash
git clone https://github.com/user/project.git
```

作用：

把远程仓库完整下载到本地，包括：

* 项目文件
* Git 历史
* 分支信息

指定本地目录：

```bash
git clone https://github.com/user/project.git my-project
```

表示下载后目录叫：

```text
my-project/
```

---

# 4. 查看代码修改

## `git diff`

```bash
git diff
```

作用：

查看：

```text
工作区
vs
暂存区
```

之间有什么变化。

例如你修改了：

```python
print("hello")
```

变成：

```python
print("hello world")
```

运行：

```bash
git diff
```

会显示类似：

```diff
-print("hello")
+print("hello world")
```

---

## 查看已经暂存的修改

```bash
git diff --staged
```

或者：

```bash
git diff --cached
```

作用：

查看：

```text
暂存区
vs
上一次 commit
```

也就是：

> 下一次 commit 准备提交什么。

---

# 5. 将修改加入暂存区

## `git add`

添加单个文件：

```bash
git add main.py
```

添加多个文件：

```bash
git add main.py utils.py
```

添加当前目录所有修改：

```bash
git add .
```

作用：

```text
工作区
↓
暂存区
```

注意：

```bash
git add .
```

不是上传 GitHub。

也不是创建 commit。

只是表示：

> 把这些修改加入下一次提交。

---

# 6. 提交代码

## `git commit`

最常用：

```bash
git commit -m "Fix login bug"
```

作用：

```text
暂存区
↓
本地仓库
```

创建一次正式的版本记录。

---

## 参数 `-m`

```bash
-m
```

表示：

```text
message
```

也就是提交说明。

例如：

```bash
git commit -m "Add user login"
```

推荐 commit message 简洁明确：

```text
Add login page
Fix recommendation bug
Update README
Refactor data loader
```

不推荐：

```text
update
change
123
test
```

---

# 7. 查看提交历史

## `git log`

```bash
git log
```

查看详细 commit 历史。

---

## 简洁显示

```bash
git log --oneline
```

输出：

```text
a81c32f Fix login bug
81f45ac Add login page
193ca21 Initial commit
```

其中：

```text
a81c32f
```

是 commit ID 的缩写。

---

## 显示所有分支图

```bash
git log --oneline --graph --all
```

非常推荐。

输出可能：

```text
* a82e9d1 Fix bug
| * 91cd322 Add login
|/
* b27a331 Initial commit
```

参数：

```text
--oneline
每个 commit 一行

--graph
以图形方式显示分支关系

--all
显示所有分支
```

推荐记住：

```bash
git log --oneline --graph --all
```

---

# 8. 查看分支

## `git branch`

```bash
git branch
```

作用：

查看本地分支。

例如：

```text
* main
  dev
  feature-login
```

`*` 表示当前所在分支。

---

## 查看远程分支

```bash
git branch -r
```

参数：

```text
-r
remote
```

例如：

```text
origin/main
origin/dev
```

---

## 查看所有分支

```bash
git branch -a
```

参数：

```text
-a
all
```

显示：

* 本地分支
* 远程分支

---

# 9. 创建分支

传统方式：

```bash
git branch feature-login
```

作用：

创建分支：
P
```text
feature-login
```

但不会自动切换过去。

---

推荐现代写法：

```bash
git switch -c feature-login
```

作用：

```text
创建 feature-login
切换到 feature-login
```

---

## 参数 `-c`

```text
-c
create
```

所以：

```bash
git switch -c dev
```

表示：

> 创建 dev 分支并切换过去。

---

# 10. 切换分支

## 推荐使用 `git switch`

```bash
git switch main
```

表示：

> 切换到 main 分支。

例如：

```bash
git switch dev
```

---

## 旧写法 `git checkout`

你以后一定会看到：

```bash
git checkout main
```

作用同样是切换到 `main`。

创建并切换：

```bash
git checkout -b feature-login
```

其中：

```text
-b
branch
```

现代 Git 更推荐：

```bash
git switch -c feature-login
```

所以学习优先级：

```text
推荐使用：
git switch

但必须认识：
git checkout
```

---

# 11. 删除分支

安全删除：

```bash
git branch -d feature-login
```

参数：

```text
-d
delete
```

如果该分支还有未合并内容，Git 会阻止删除。

---

强制删除：

```bash
git branch -D feature-login
```

`-D` 表示强制删除。

要谨慎使用。

---

# 12. 合并分支

假设你有：

```text
main
feature-login
```

你已经在 `feature-login` 写好了功能。

首先：

```bash
git switch main
```

然后：

```bash
git merge feature-login
```

意思是：

```text
把 feature-login
合并到
当前分支 main
```

非常重要：

```bash
git merge feature-login
```

不是：

> 把 main 合并到 feature-login

而是：

> 把 feature-login 合并进“当前所在分支”。

所以先看：

```bash
git branch
```

确认自己在哪。

---

# 13. 查看远程仓库

## `git remote`

```bash
git remote
```

可能显示：

```text
origin
```

`origin` 通常表示：

> 默认远程仓库的名字。

---

## 查看详细地址

```bash
git remote -v
```

参数：

```text
-v
verbose
```

输出：

```text
origin  https://github.com/user/project.git (fetch)
origin  https://github.com/user/project.git (push)
```

---

# 14. 添加远程仓库

如果本地项目刚刚：

```bash
git init
```

然后你在 GitHub 新建了一个仓库，需要连接：

```bash
git remote add origin <仓库地址>
```

例如：

```bash
git remote add origin https://github.com/user/project.git
```

含义：

```text
remote
操作远程仓库

add
添加

origin
给这个远程仓库起名叫 origin
```

---

# 15. 推送到 GitHub

## `git push`

第一次推送通常：

```bash
git push -u origin main
```

含义：

```text
把本地 main
推送到
origin 的 main
```

---

## 参数 `-u`

```text
-u
--set-upstream
```

表示建立跟踪关系。

第一次执行：

```bash
git push -u origin main
```

以后通常只需要：

```bash
git push
```

---

# 16. 从远程获取更新

## `git fetch`

```bash
git fetch
```

作用：

从远程仓库获取最新信息，但是：

> 不会直接修改你的工作区代码。

可以理解为：

```text
GitHub
↓
更新 origin/main 等远程信息
↓
本地代码暂时不变
```

更安全，适合先看看远程发生了什么。

---

# 17. 拉取远程代码

## `git pull`

```bash
git pull
```

大致可以理解为：

```text
git fetch
+
git merge
```

也就是：

```text
从远程获取更新
+
合并到当前分支
```

例如你和别人合作：

```bash
git switch main
git pull
```

让你的本地 `main` 更新到最新状态。

---

# 18. `fetch` 和 `pull` 区别

```text
git fetch
↓
下载远程更新
但不合并


git pull
↓
下载远程更新
并自动合并
```

所以初学阶段可以理解：

```text
想安全查看远程变化
→ git fetch

想直接同步最新代码
→ git pull
```

---

# 19. 恢复工作区修改

## `git restore`

假设你修改了：

```text
main.py
```

但是发现改错了，想恢复到之前：

```bash
git restore main.py
```

作用：

> 放弃 main.py 当前工作区修改。

注意：

可能导致代码修改丢失。

执行前建议：

```bash
git diff
```

确认。

---

## 恢复所有工作区修改

```bash
git restore .
```

非常危险。

表示：

> 丢弃当前目录所有未暂存修改。

---

# 20. 将文件移出暂存区

假设：

```bash
git add main.py
```

之后后悔了。

执行：

```bash
git restore --staged main.py
```

作用：

```text
暂存区
↓
移回工作区
```

但是：

> 不会删除你写的代码。

例如：

```text
修改 main.py
↓
git add main.py
↓
进入暂存区
↓
git restore --staged main.py
↓
退出暂存区
但修改还在
```

---

# 21. 临时保存修改

## `git stash`

假设：

你正在 `dev` 上写代码，但是代码还没写完。

突然需要切去 `main` 修 Bug。

可以：

```bash
git stash
```

作用：

> 临时保存当前修改，让工作区变干净。

然后：

```bash
git switch main
```

修完之后：

```bash
git switch dev
```

恢复修改：

```bash
git stash pop
```

完整流程：

```bash
git stash
git switch main

# 修 bug

git switch dev
git stash pop
```

---

## 查看 stash

```bash
git stash list
```

---

# 22. GitHub 日常标准流程

假设你接到一个 Issue：

```text
Issue #23
Fix recommendation bug
```

推荐流程：

```bash
git switch main
git pull

git switch -c fix-issue-23
```

然后写代码。

查看修改：

```bash
git status
git diff
```

加入暂存区：

```bash
git add .
```

检查：

```bash
git diff --staged
```

提交：

```bash
git commit -m "Fix recommendation bug"
```

推送：

```bash
git push -u origin fix-issue-23
```

然后去 GitHub：

```text
Create Pull Request
```

最后：

```text
Code Review
↓
Merge
↓
Issue Closed
```

---

# 23. `.gitignore`

项目中通常：

```text
.gitignore
```

用于告诉 Git：

> 哪些文件不要跟踪。

Python 项目常见：

```gitignore
# Python cache
__pycache__/
*.pyc

# Virtual environment
.venv/
venv/

# VS Code
.vscode/

# Secrets
.env
```

注意：

`.gitignore` 只对：

> 尚未被 Git 跟踪的文件

最直接。

如果一个文件已经 commit 过，仅加入 `.gitignore` 不会自动停止跟踪。

---

# 24. 当前阶段需要真正熟练的命令

## 第一优先级

必须熟练：

```bash
git status

git init
git clone

git add .
git add <文件>

git commit -m "message"

git log --oneline

git diff
git diff --staged

git branch
git switch <分支>
git switch -c <新分支>

git merge <分支>

git pull
git push

git remote -v
```

---

## 第二优先级

需要理解并会使用：

```bash
git branch -a
git branch -r

git branch -d <分支>

git fetch

git restore <文件>
git restore --staged <文件>

git stash
git stash pop
git stash list
```

---

## 第三优先级

现在先认识，以后再深入：

```bash
git rebase
git reset
git revert
git cherry-pick
git reflog
git tag
```

这些暂时不需要急着背。

---

# 25. 参数速查

```text
-m
message
提交说明

-c
create
创建分支

-d
delete
安全删除分支

-D
强制删除分支

-r
remote
远程分支

-a
all
所有分支

-v
verbose
显示详细信息

-u
set upstream
建立本地分支与远程分支的跟踪关系

--oneline
commit 每条显示一行

--graph
显示分支图

--all
显示所有分支

--staged
查看或操作暂存区
```

---

# 26. 最值得记住的一套命令

日常开发：

```bash
git status
git diff

git add .

git diff --staged

git commit -m "Fix bug"

git push
```

---

新功能开发：

```bash
git switch main
git pull

git switch -c feature-login

# 修改代码

git add .
git commit -m "Add login feature"

git push -u origin feature-login
```

---

功能完成以后：

```bash
git switch main
git pull

git merge feature-login

git push
```

如果在 GitHub 使用 Pull Request，通常会在 GitHub 网页完成 merge。

---

# 27. Git 最核心的理解

不要只背：

```text
add
commit
push
```

而要真正理解：

```text
工作区
你正在修改的代码

↓ git add

暂存区
下一次 commit 准备提交的内容

↓ git commit

本地仓库
正式的版本历史

↓ git push

远程仓库
GitHub 上的版本
```

同时：

```text
main
dev
feature-login
```

这些都是：

> 指向某些 commit 的分支。

所以 Git 本质上是在管理：

```text
文件修改
+
提交历史
+
分支关系
+
本地与远程同步
```
