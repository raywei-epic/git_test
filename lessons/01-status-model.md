# 01. 先理解 Git 的三个位置

在开始 `git stash` 前，先记住这三个位置：

- 工作区：你正在编辑、还没有确认保存到 Git 历史里的内容。
- 暂存区：你用 `git add` 挑出来，准备进入下一次提交的内容。
- 提交历史：你已经用 `git commit` 保存下来的版本。

## 练习 A：观察工作区

修改 `app.txt`，例如把：

```text
- improve help text
```

改成：

```text
- improve help text for new users
```

然后运行：

```bash
git status
git diff
```

你应该能看到：文件被修改了，但还没有进入暂存区。

## 练习 B：观察暂存区

继续运行：

```bash
git add app.txt
git status
git diff
git diff --staged
```

重点观察：

- `git diff` 看未暂存的修改。
- `git diff --staged` 看已经放入暂存区、准备提交的修改。

## 练习 C：提交一个完整小成果

```bash
git commit -m "Update app help text"
git status
```

如果 `git status` 显示 `working tree clean`，说明当前没有未提交修改。

## 关键理解

`git stash` 处理的是“还没有提交”的修改。你越能看懂 `git status`，越容易理解 stash。
