# 练习场景索引

这里把练习拆成几个任务卡。建议每次只做一个任务卡，做完后运行 `git status` 看仓库状态。

## 任务卡 1：看懂 status

目标：知道工作区、暂存区、提交历史分别在哪里。

材料：`lessons/01-status-model.md`

完成标准：

- 能解释 `git diff` 和 `git diff --staged` 的区别。
- 能把一个小修改提交成 commit。
- 能让 `git status` 回到干净状态。

## 任务卡 2：第一次 stash

目标：把做到一半的修改收起来，再恢复回来。

材料：`lessons/02-stash-basic.md`

完成标准：

- 能用 `git stash list` 找到 stash。
- 能用 `git stash show -p` 查看 stash 内容。
- 能说出 `apply` 和 `pop` 的区别。

## 任务卡 3：临时切分支

目标：模拟“功能做到一半，先切去修 bug”的真实工作节奏。

材料：`lessons/03-real-workflow.md`

完成标准：

- 能在修改未提交时用 stash 清理工作区。
- 能切分支，再回到原分支恢复 stash。
- 能给 stash 写清楚说明信息。

## 任务卡 4：新文件和冲突

目标：理解普通 stash、`stash -u`、stash 冲突的区别。

材料：`lessons/03-real-workflow.md`

完成标准：

- 知道未跟踪文件为什么普通 stash 不会收走。
- 会用 `git stash -u`。
- 遇到冲突时先运行 `git status`，再手动解决冲突标记。

## 任务卡 5：同步远端代码

目标：理解本地分支和远端分支的关系，知道开发前为什么要同步。

材料：`lessons/04-sync-remote-work.md`

完成标准：

- 能说出 `git fetch` 和 `git pull` 的区别。
- 能用 `git log --oneline --graph --decorate --all` 观察分支关系。
- 能解释 ahead、behind、diverged 大概是什么意思。

## 任务卡 6：功能分支与 PR 前准备

目标：从主分支切出功能分支，完成一个小修改并检查提交状态。

材料：`lessons/05-branch-and-pr-workflow.md`

完成标准：

- 能用 `git switch -c` 创建功能分支。
- 能在提交前用 `git diff` 检查修改。
- 能在准备 PR 前确认 `git status` 是干净的。

## 任务卡 7：解决合并冲突

目标：制造一次合并冲突，并完整走完解决流程。

材料：`lessons/06-resolve-merge-conflict.md`

完成标准：

- 能看懂 `<<<<<<<`、`=======`、`>>>>>>>` 冲突标记。
- 能手动决定最终内容并删除冲突标记。
- 能用 `git add` 和 `git commit` 完成一次冲突解决。

## 任务卡 8：撤销常见误操作

目标：掌握工作区、暂存区、最近一次提交的常见撤销方式。

材料：`lessons/07-undo-common-mistakes.md`

完成标准：

- 能用 `git restore` 丢弃确认不要的工作区修改。
- 能用 `git restore --staged` 取消暂存但保留文件内容。
- 能说明什么时候可以安全使用 `git commit --amend`。

## 任务卡 9：整理提交历史

目标：理解 PR 前为什么要整理提交历史，以及什么时候不能随便改历史。

材料：`lessons/08-clean-commit-history.md`

完成标准：

- 能用 `git log --oneline` 找到零碎 commit。
- 能解释 `amend` 和 `squash` 分别解决什么问题。
- 能说出为什么不要随便改共享分支的历史。

## 重置练习仓库

如果你想重新开始练习，先确认这里没有重要内容，然后运行：

```bash
git status
git stash list
```

如果只是想回到最后一次提交：

```bash
git reset --hard
```

注意：这个命令会丢弃当前未提交修改，只应该在这个练习仓库里使用。
