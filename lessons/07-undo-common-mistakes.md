# 07. 撤销常见误操作

真实工程里，最常见的 Git 紧张时刻不是大事故，而是这些小问题：

> 改错文件、误加到暂存区、提交信息写错、刚提交就发现漏了一行。

这一节只练习相对常用、比较安全的撤销方式。

## 练习 A：撤销工作区里的误改

先修改 `app.txt`，随便加一行：

```text
- temporary wrong change
```

查看修改：

```bash
git status
git diff
```

如果确认这次修改不要了，运行：

```bash
git restore app.txt
git status
```

`git restore app.txt` 的意思是：

```text
把 app.txt 在工作区里的未暂存修改丢掉。
```

注意：这会丢弃文件里的未保存到 Git 历史的修改，只在你确认不要时使用。

## 练习 B：取消暂存，但保留文件修改

再修改 `app.txt`，加入：

```text
- draft help copy
```

把它放进暂存区：

```bash
git add app.txt
git status
```

现在取消暂存：

```bash
git restore --staged app.txt
git status
git diff
```

你会看到修改还在文件里，只是不再处于 staged 状态。

这适合这种情况：

> 我刚才 `git add` 加早了，想重新检查或拆分提交。

## 练习 C：改最近一次提交信息

先提交一个小修改：

```bash
git add app.txt
git commit -m "Wip"
```

如果只是提交信息写得太随意，而且这个 commit 还没有推给别人，可以运行：

```bash
git commit --amend -m "Update help page draft"
```

然后查看：

```bash
git log --oneline -n 3
```

注意：`--amend` 会替换最近一次 commit。已经推到共享远端的提交，不要随便 amend。

## 练习 D：刚提交发现漏改一行

假设你刚提交完，发现还漏了一行。继续修改 `app.txt`，加入：

```text
- add missing help detail
```

然后运行：

```bash
git add app.txt
git commit --amend
```

这会把新修改合进最近一次提交。

如果打开编辑器，确认提交信息没问题后保存退出。

## 常见判断

- 文件改错了，还没 `git add`：用 `git restore 文件名`。
- 文件 `add` 早了，但内容还想保留：用 `git restore --staged 文件名`。
- 最近一次提交信息写错，且还没推给别人：可以用 `git commit --amend -m "新信息"`。
- 最近一次提交漏改内容，且还没推给别人：补改后 `git add`，再 `git commit --amend`。

## 关键理解

撤销前先问自己两个问题：

1. 这个修改是在工作区、暂存区，还是已经进入提交历史？
2. 这个提交有没有推给别人？

位置不同，安全做法也不同。
