# 03. 模拟真实工作流

这一节模拟一个常见工作场景：

> 你正在开发个人资料页，突然有人让你切去修首页文案 bug。你不想把半成品提交，于是用 `git stash` 暂存现场。

## 场景 A：功能做到一半，需要临时切分支

先创建功能分支：

```bash
git switch -c feature/profile
```

修改 `app.txt`，加入：

```text
Profile page:
- show user name
- show user bio
```

查看状态：

```bash
git status
```

现在你有未提交修改，还不适合提交。

把现场收起来：

```bash
git stash push -m "WIP profile page"
git status
```

切回主分支处理 bug：

```bash
git switch master
```

修完 bug 后，再回到功能分支：

```bash
git switch feature/profile
git stash list
git stash apply
```

如果在错误的分支执行了git stash pop：
```bash
git reset --hard HEAD
```

## 场景 B：新文件默认不会被普通 stash 保存

创建一个新文件：

```bash
echo "temporary notes" > local-notes.txt
git status
git stash
git status
```

你会发现未跟踪的新文件通常还在工作区里。

如果新文件也要一起收起来，用：

```bash
git stash -u
```

其中 `-u` 表示 include untracked files。

## 场景 C：制造一次 stash 冲突

先保证工作区干净：

```bash
git status
```

如果不干净，先提交、丢弃或 stash 掉当前练习修改。

然后修改 `app.txt` 中的标题，例如：

```text
- title: Git practice app from stash
```

保存到 stash：

```bash
git stash push -m "change title from stash"
```

接着在当前文件里把同一行改成另一个版本：

```text
- title: Git practice app from branch
```

提交这个修改：

```bash
git add app.txt
git commit -m "Change title on branch"
```

现在恢复 stash：

```bash
git stash pop
```

大概率会出现冲突。此时不要慌，运行：

```bash
git status
```

打开冲突文件，你会看到类似：

```text
<<<<<<< Updated upstream
- title: Git practice app from branch
=======
- title: Git practice app from stash
>>>>>>> Stashed changes
```

手动改成你想保留的结果，删除冲突标记，然后：

```bash
git add app.txt
git commit -m "Resolve stash conflict"
```

## 工作中怎么判断

- 半成品、只是临时让开现场：stash。
- 已经完成一个独立小任务：commit。
- 是另一个长期任务：新建分支。
- 要保存新文件：stash 加 `-u`。
