# Git Stash 小抄

## 最常用命令

```bash
git stash
```

把当前已跟踪文件的未提交修改临时收起来。

```bash
git stash push -m "message"
```

带说明地保存 stash，推荐在工作中使用。

```bash
git stash list
```

查看所有 stash。

```bash
git stash show
git stash show -p
```

查看最近一条 stash 的摘要或完整 diff。

```bash
git stash apply
```

恢复最近一条 stash，但保留 stash 记录。

```bash
git stash pop
```

恢复最近一条 stash，并在成功后删除 stash 记录。

```bash
git stash drop
```

删除最近一条 stash。

```bash
git stash -u
```

连未跟踪的新文件也一起 stash。

## 指定某一条 stash

```bash
git stash apply stash@{1}
git stash drop stash@{1}
```

`stash@{0}` 是最新的一条，数字越大越旧。

## pop 和 apply 的区别

- `apply`：恢复，但不删除 stash，更稳。
- `pop`：恢复，并在成功后删除 stash，更快。

初学时建议先用 `apply`，确认没问题再 `drop`。

## 常见误区

- stash 不是 commit，不会出现在普通提交历史里。
- stash 不适合长期保存重要工作。
- 普通 `git stash` 不保存未跟踪文件，新文件要用 `git stash -u`。
- 恢复 stash 也可能冲突，处理方式和普通 merge 冲突类似。

## 遇到问题先跑

```bash
git status
git stash list
```
