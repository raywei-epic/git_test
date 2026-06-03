# 05. 功能分支与 PR 前准备

真实工程里，很少直接在主分支上写功能。更常见的节奏是：

> 从主分支切出一个功能分支，在分支上完成小任务，再提交给团队 review。

这一节模拟“新增帮助页文案”的小功能。

## 练习 A：从干净状态开始

先运行：

```bash
git status
git branch
```

如果工作区不干净，先处理当前修改：

- 已经完成的小成果：提交。
- 半成品：stash。
- 练习中不要的修改：确认无用后再丢弃。

## 练习 B：创建功能分支

运行：

```bash
git switch -c feature/help-page
git branch
```

你应该能看到当前分支变成了 `feature/help-page`。

分支名建议表达任务目的，例如：

```text
feature/help-page
fix/home-title
docs/git-lessons
```

## 练习 C：删除功能分支

运行：

```bash
git switch -d feature/delete
git push origin --delete feature/delete
```


## 练习 D：完成一个小功能

修改 `app.txt`，加入：

```text
Help page:
- explain basic navigation
- show contact email
```

然后运行：

```bash
git status
git diff
```

确认修改内容符合预期后提交：

```bash
git add app.txt
git commit -m "Add help page notes"
```

## 练习 E：检查 PR 前状态

运行：

```bash
git status
git log --oneline --decorate -n 5
```

PR 前至少确认三件事：

- `git status` 没有意外的未提交修改。
- commit 信息能说明这次改动的目的。
- 分支名能让 reviewer 大概知道你在做什么。

## 练习 F：回到主分支

运行：

```bash
git switch master
git status
```

如果你的仓库主分支叫 `main`，就改成：

```bash
git switch main
```

回到主分支后，`app.txt` 可能不会显示刚才功能分支上的内容。这是正常的，因为那次修改属于 `feature/help-page` 分支。

## 工作中怎么判断

- 新功能、修 bug、文档修改，都适合单独开分支。
- 一个分支最好围绕一个清晰目标，不要混进多个无关任务。
- 提交前先看 `git diff`，提交后再看 `git status`。
- 准备 PR 前，先确认工作区干净。
