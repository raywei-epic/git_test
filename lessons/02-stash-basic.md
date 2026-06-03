# 02. Git Stash 基础练习

`git stash` 的作用是：把当前未提交的修改临时收起来，让工作区恢复干净。

它适合这种场景：

> 你功能做到一半，还不适合提交，但突然需要切到别的分支处理事情。

## 练习 A：把做到一半的修改收起来

修改 `app.txt`，在 `Todo` 下增加一行：

```text
- add settings page
```

然后运行：

```bash
git status
git stash
git status
git stash list
```

你会看到：

- `git stash` 前，`app.txt` 是 modified。
- `git stash` 后，工作区变干净。
- `git stash list` 能看到刚刚保存的 stash。

## 练习 B：查看 stash 里有什么

```bash
git stash show
git stash show -p
```

区别：

- `git stash show` 只看文件级摘要。
- `git stash show -p` 看具体 diff。

## 练习 C：恢复 stash

先用：

```bash
git stash apply
git status
```

`apply` 会恢复修改，但 stash 记录仍然保留。

再运行：

```bash
git stash list
git stash drop
git stash list
```

`drop` 会删除那条 stash 记录。

## 练习 D：理解 pop

重新制造一次修改，然后运行：

```bash
git stash
git stash pop
git stash list
```

`pop` 相当于：

```text
apply + drop
```

也就是恢复修改，并在成功后删除 stash 记录。

## apply 和 pop 怎么选

- 想保险一点：用 `git stash apply`，确认没问题后再 `git stash drop`。
- 很确定只需要恢复一次：用 `git stash pop`。
