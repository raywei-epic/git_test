# 06. 解决合并冲突

真实工程里，冲突最常见的原因是：

> 你和别人改了同一个文件的同一块内容，Git 不知道最终应该保留哪一个版本。

冲突不是 Git 坏了，而是 Git 在提醒：这里需要人来判断。

## 练习 A：准备一个冲突分支

先确认工作区干净：

```bash
git status
```

然后从主分支创建一个分支：

```bash
git switch master
git switch -c feature/title-from-feature
```

如果你的主分支叫 `main`，第一条命令改成：

```bash
git switch main
```

修改 `app.txt` 的标题：

```text
- title: Git practice app from feature
```

提交这个修改：

```bash
git add app.txt
git commit -m "Change title from feature branch"
```

## 练习 B：在主分支制造另一个修改

切回主分支：

```bash
git switch master
```

如果你的主分支叫 `main`，就运行：

```bash
git switch main
```

把 `app.txt` 的同一行标题改成：

```text
- title: Git practice app from main
```

提交：

```bash
git add app.txt
git commit -m "Change title from main branch"
```

## 练习 C：合并并触发冲突

现在把功能分支合进来：

```bash
git merge feature/title-from-feature
```

你大概率会看到 conflict 提示。

先不要急着乱改，运行：

```bash
git status
```

`git status` 会告诉你哪些文件处于冲突状态。

## 练习 D：看懂冲突标记

打开 `app.txt`，你会看到类似：

```text
<<<<<<< HEAD
- title: Git practice app from main
=======
- title: Git practice app from feature
>>>>>>> feature/title-from-feature
```

含义是：

- `<<<<<<< HEAD` 到 `=======` 之间，是当前分支的版本。
- `=======` 到 `>>>>>>> ...` 之间，是被合并分支的版本。
- 你要手动决定最终保留什么。

例如可以改成：

```text
- title: Git practice app for real workflows
```

记得删除所有冲突标记。

## 练习 E：完成合并

解决完文件内容后运行：

```bash
git add app.txt
git status
git commit
```

如果 Git 自动打开编辑器，保留默认 merge commit 信息也可以。

完成后检查：

```bash
git status
git log --oneline --graph --decorate -n 8
```

## 如果想放弃这次 merge

如果你只是练习，合并到一半不想继续，可以运行：

```bash
git merge --abort
```

它会尽量把仓库恢复到 merge 开始前的状态。

## 关键理解

- 冲突文件里必须删除 `<<<<<<<`、`=======`、`>>>>>>>` 这些标记。
- 解决冲突后要 `git add`，表示“这个冲突我处理完了”。
- `git status` 是冲突期间最重要的导航命令。
- 不确定怎么解决内容时，先和同事确认业务结果，而不是只选自己的版本。
