# 08. 整理提交历史

真实工程里，开发一个功能时常会出现这种历史：

```text
add profile title
fix typo
try another wording
fix again
```

这些 commit 记录了你的尝试过程，但 reviewer 更关心最终改动是否清晰。

这一节练习 PR 前如何看懂并整理自己的提交历史。

## 练习 A：先看历史

运行：

```bash
git log --oneline --decorate -n 8
```

重点观察：

- 最近几个 commit 分别做了什么。
- 有没有明显的 `fix typo`、`wip`、`fix again`。
- 有没有多个 commit 其实属于同一个小目标。

## 练习 B：制造几个零碎提交

创建一个练习分支：

```bash
git switch -c feature/clean-history
```

第一次修改 `app.txt`，加入：

```text
Settings page:
- allow profile updates
```

提交：

```bash
git add app.txt
git commit -m "Add settings page notes"
```

继续修改同一段内容，加入：

```text
- allow notification preferences
```

提交：

```bash
git add app.txt
git commit -m "Fix settings notes"
```

现在查看历史：

```bash
git log --oneline --decorate -n 5
```

你会看到两个 commit，其实都在服务同一个目标：补充 settings page notes。

## 练习 C：用 amend 整理最近一次提交

如果你只是刚提交完，发现最后一个 commit 信息不好，可以用：

```bash
git commit --amend -m "Update settings page notes"
```

然后查看：

```bash
git log --oneline --decorate -n 5
```

`amend` 只适合处理最近一次提交。

## 练习 D：理解 squash 的目的

如果多个 commit 都属于同一个目标，PR 前可能会把它们合并成一个更清晰的 commit。

这个动作通常叫：

```text
squash
```

它的目的不是隐藏错误，而是让项目历史更容易阅读。

例如：

```text
Add settings page notes
Fix settings notes
```

可以整理成：

```text
Update settings page notes
```

## 练习 E：什么时候不要改历史

在真实项目里，历史整理有一条重要边界：

```text
不要随便改已经推给别人并且可能被别人基于其继续工作的提交。
```

适合整理的情况：

- 你自己的功能分支。
- 还没有推到远端。
- 或团队明确允许在 PR 分支上整理历史。

不适合随便整理的情况：

- 主分支。
- 发布分支。
- 多个人正在共同使用的共享分支。

## 更保守的做法

如果你不确定能不能改历史，不要急着用复杂命令。

你可以先做到：

```bash
git log --oneline --decorate -n 8
git status
```

然后在 PR 描述里说明：

```text
前几个 commit 是开发过程中的中间提交，最终改动以整体 diff 为准。
```

在团队允许时，再学习 `git rebase -i` 或平台提供的 squash merge。

## 关键理解

- 整理历史前，先看 `git log`。
- `amend` 用来替换最近一次提交。
- `squash` 用来把多个相关 commit 合成一个。
- 改历史前先确认：这个分支是不是只有你自己在用。
