# 04. 同步远端代码

真实工程里，开始写代码前经常先做一件事：

> 确认自己的本地分支没有落后远端，避免基于旧代码继续开发。

这一节重点不是记命令，而是看懂“本地”和“远端”的关系。

## 练习 A：先看当前连接了哪些远端仓库

运行：

```bash
git remote -v
git status
```

如果能看到 `origin`，说明当前仓库连接了一个远端仓库。

如果没有任何输出，也没关系。说明这个练习仓库暂时还没有远端，你仍然可以先理解命令含义。

## 练习 B：用 fetch 更新远端信息

运行：

```bash
git fetch
git status
```

`git fetch` 的作用是：

```text
把远端最新信息取回来，但不直接改你的工作区文件。
```

所以它比 `git pull` 更适合用来“先看看远端发生了什么”。

## 练习 C：查看本地和远端的提交关系

运行：

```bash
git log --oneline --graph --decorate --all -n 10
```

重点观察：

- 当前分支名通常会显示在 `HEAD -> 分支名` 附近。
- 远端分支通常会显示成 `origin/master` 或 `origin/main`。
- 如果本地分支和远端分支指向同一个提交，说明它们暂时同步。
- 如果位置不同，说明本地和远端已经出现领先或落后。

## 练习 D：理解 pull 做了什么

运行：

```bash
git pull
git status
```

`git pull` 通常相当于：

```text
git fetch + 把远端变化合进当前分支
```

如果你当前有未提交修改，`git pull` 可能会被拒绝，或者引发冲突。

所以真实工作中更稳的顺序是：

```bash
git status
git fetch
git log --oneline --graph --decorate --all -n 10
git pull
```

## 看到 ahead 和 behind 时怎么办

如果 `git status` 提示：

```text
Your branch is ahead of 'origin/master'
```

说明你本地有提交还没有推到远端。

如果提示：

```text
Your branch is behind 'origin/master'
```

说明远端有新提交，你本地还没有同步。

如果提示：

```text
Your branch and 'origin/master' have diverged
```

说明本地和远端各自都有新提交，需要先看清楚历史，再决定 merge、rebase 或请同事确认。

## 关键理解

- `fetch` 是更新远端信息，不直接改工作区。
- `pull` 会尝试把远端变化合进当前分支。
- 开始开发前先 `git status`，再同步远端。
- 不确定历史关系时，用 `git log --oneline --graph --decorate --all` 看图。
