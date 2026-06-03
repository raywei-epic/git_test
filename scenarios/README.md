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
