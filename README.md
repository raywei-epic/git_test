# Git Engineering Practice

这是一个用来练习真实工程 Git 场景的小仓库。你可以放心修改、提交、stash、切分支、制造冲突，因为它和你的真实工作仓库是分开的。

建议学习顺序：

1. 先看 `lessons/01-status-model.md`，理解工作区、暂存区、提交历史。
2. 再看 `lessons/02-stash-basic.md`，练习 `stash` 的基础命令。
3. 看 `lessons/03-real-workflow.md`，模拟工作中临时切分支和处理 stash 冲突。
4. 看 `lessons/04-sync-remote-work.md`，理解同步远端代码时的 `fetch`、`pull`、领先和落后。
5. 看 `lessons/05-branch-and-pr-workflow.md`，练习功能分支和 PR 前准备。
6. 看 `lessons/06-resolve-merge-conflict.md`，练习制造并解决合并冲突。
7. 看 `lessons/07-undo-common-mistakes.md`，练习撤销误改、取消暂存和修正最近一次提交。
8. 看 `lessons/08-clean-commit-history.md`，理解 PR 前整理提交历史的基本判断。
9. 忘记 stash 命令时看 `STASH-CHEATSHEET.md`。

练习时最重要的一条规则：

```bash
git status
```

不确定当前发生了什么时，先看状态，再决定下一步。
