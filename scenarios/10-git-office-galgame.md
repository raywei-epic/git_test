# 任务卡 10：Git 职场 Galgame 综合演练

> 类型：剧情交互式 Git 任务
>
> 主题：入职第一周，你在团队项目里完成一个小功能，中途被线上 bug、同事提交、冲突和 PR review 打断。
>
> 建议：每完成一幕都运行一次 `git status`。如果你不确定现在发生了什么，先停下来读 `git status` 的提示。

## 登场角色

- 你：刚入职的开发者，负责改进 `Mini App` 的帮助和设置文案。
- 林姐：你的 mentor，习惯在你快要乱按命令时提醒你先看状态。
- 阿南：后端同事，经常在你开发中途推新代码。
- 小夏：测试同事，会突然报告线上文案 bug。
- Reviewer：PR 审查人，只关心最终 diff 是否清楚、commit 是否能读懂。

## 开始前确认

先确认你在练习仓库里：

```bash
pwd
git status
git branch
```

如果当前工作区不干净，先决定：

- 已经完成的小成果：提交。
- 只是半成品：stash。
- 明确不要的练习修改：确认后再丢弃。

不要在真实工作仓库里随便执行本剧本里的练习命令。

## 序章：周一早会后的第一张卡

林姐把任务卡推到你面前：

> “今天你负责把帮助页文案补完整。第一步，不是写代码，是确认仓库状态。”

### 你的行动

```bash
git status
git diff
git diff --staged
```

### 选择

- A. `git status` 显示干净：进入第一幕。
- B. 有 modified 文件：先用 `git diff` 看看是不是你要保留的修改。
- C. 有 staged 文件：用 `git diff --staged` 确认它们是不是准备进入下一次提交。

### 检查点

你需要能说清楚：

- 工作区：正在编辑、还没进入 Git 历史的内容。
- 暂存区：已经 `git add`，准备提交的内容。
- 提交历史：已经 `git commit` 保存过的版本。

对应课程：`lessons/01-status-model.md`

## 第一幕：创建你的功能分支

你正准备修改 `app.txt`，林姐在旁边说：

> “不要直接在主分支上做功能。给这张任务卡一个自己的分支。”

### 你的行动

先确认主分支名称。如果你的主分支叫 `master`：

```bash
git switch master
git switch -c feature/help-copy-galgame
```

如果你的主分支叫 `main`：

```bash
git switch main
git switch -c feature/help-copy-galgame
```

然后修改 `app.txt`，在 `Help` 或 `Todo` 附近加入类似内容：

```text
Help page:
- explain basic navigation
- show contact email
```

查看修改：

```bash
git status
git diff
```

### 选择

- A. 修改符合预期：`git add app.txt`，但先不要提交，进入第二幕。
- B. 改错了文件：用 `git restore 文件名` 撤销确认不要的工作区修改。
- C. 还想继续改：保持 modified 状态，进入第二幕。

### 检查点

你应该能用 `git diff` 解释自己改了什么，并知道这时修改还没有进入提交历史。

对应课程：`lessons/01-status-model.md`、`lessons/05-branch-and-pr-workflow.md`

## 第二幕：线上 bug 打断了你

小夏突然发来消息：

> “首页标题文案显示不对，能不能先修一下？这个要马上发。”

你看着半成品帮助页，知道它还不适合提交。

### 你的行动

如果你刚才已经 `git add app.txt`，先观察暂存区：

```bash
git status
git diff --staged
```

把半成品收起来：

```bash
git stash push -m "WIP help copy before hotfix"
git status
git stash list
git stash show -p
```

切回主分支，再开 hotfix 分支：

```bash
git switch master
git switch -c fix/home-title-copy
```

如果你的主分支叫 `main`，第一条命令改成：

```bash
git switch main
```

修改 `app.txt` 的标题文案，例如：

```text
- title: Git practice app for daily work
```

提交 hotfix：

```bash
git status
git diff
git add app.txt
git commit -m "Fix home title copy"
```

### 选择

- A. 你想稳一点恢复 stash：后面用 `git stash apply`，确认无误后再 `git stash drop`。
- B. 你确定只恢复一次：后面可以用 `git stash pop`。

### 检查点

你需要能说出：

- `git stash list` 用来看有哪些 stash。
- `git stash show -p` 用来看 stash 里的具体 diff。
- `apply` 会恢复修改但保留 stash 记录。
- `pop` 相当于成功恢复后再删除 stash 记录。

对应课程：`lessons/02-stash-basic.md`、`lessons/03-real-workflow.md`

## 第三幕：回到原来的功能任务

hotfix 处理完了，林姐点点头：

> “现在把你刚才的帮助页工作现场找回来。记得回到正确分支再恢复。”

### 你的行动

```bash
git switch feature/help-copy-galgame
git stash list
git stash show -p
git stash apply
git status
```

确认帮助页修改恢复成功后，如果你不再需要那条 stash：

```bash
git stash drop
git stash list
```

如果你选择使用 `pop`：

```bash
git stash pop
git stash list
```

### 如果出现冲突

先不要乱改，运行：

```bash
git status
```

打开冲突文件，找到类似内容：

```text
<<<<<<< Updated upstream
当前分支里的内容
=======
stash 里的内容
>>>>>>> Stashed changes
```

手动决定最终内容，删除所有冲突标记，然后：

```bash
git add app.txt
git commit -m "Resolve help copy stash conflict"
```

### 检查点

你需要能解释为什么“先切回正确分支，再恢复 stash”很重要。

对应课程：`lessons/02-stash-basic.md`、`lessons/03-real-workflow.md`

## 第四幕：未跟踪文件的陷阱

你一边改文案，一边写了本地笔记：

```bash
echo "QA asked to mention contact email" > local-notes.txt
git status
```

林姐问：

> “如果现在普通 `git stash`，这个新文件会被收起来吗？”

### 你的行动

先试普通 stash：

```bash
git stash push -m "WIP help copy without untracked"
git status
```

观察 `local-notes.txt` 是否还在工作区。

如果你希望未跟踪文件也一起保存：

```bash
git stash push -u -m "WIP help copy with notes"
git status
git stash list
```

恢复时仍然建议先看：

```bash
git stash show -p
git stash apply
```

### 检查点

你需要知道：

- 普通 `git stash` 通常不会保存未跟踪文件。
- `git stash -u` 或 `git stash push -u` 会包含 untracked files。

对应课程：`lessons/03-real-workflow.md`

## 第五幕：阿南推了新代码

阿南在群里说：

> “我刚把导航相关修改推上去了，你们开发前同步一下。”

你不确定自己的本地分支和远端是什么关系。

### 你的行动

```bash
git remote -v
git status
git fetch
git log --oneline --graph --decorate --all -n 10
```

如果仓库没有远端，`git remote -v` 可能没有输出，`git fetch` 也可能无法执行。这个练习点仍然是理解命令含义。

如果有远端，并且你确认要把远端变化合进当前分支：

```bash
git pull
git status
```

### 剧情提示

- `fetch`：先把远端信息取回来，不直接改你的工作区文件。
- `pull`：通常相当于 `fetch` 加“把远端变化合进当前分支”。
- ahead：你本地有提交还没推到远端。
- behind：远端有提交你本地还没有。
- diverged：本地和远端各自都有新提交，需要先看历史再决定。

### 检查点

你需要能用 `git log --oneline --graph --decorate --all` 大概看懂本地和远端分支的位置。

对应课程：`lessons/04-sync-remote-work.md`

## 第六幕：同一行的冲突

Reviewer 还没来，冲突先来了。你和阿南都改了 `app.txt` 的同一块文案。

### 你的行动：制造一次本地 merge 冲突

先保证工作区干净：

```bash
git status
```

如果还有未完成的帮助页修改，先提交：

```bash
git add app.txt
git commit -m "Update help page copy"
```

从主分支创建一个模拟同事修改的分支：

```bash
git switch master
git switch -c feature/nav-copy-from-anan
```

如果你的主分支叫 `main`，第一条命令改成：

```bash
git switch main
```

修改 `app.txt` 中同一行标题，例如：

```text
- title: Git practice app from Anan
```

提交：

```bash
git add app.txt
git commit -m "Change title from Anan"
```

回到主分支，制造另一种标题：

```bash
git switch master
```

如果你的主分支叫 `main`，改成：

```bash
git switch main
```

修改同一行：

```text
- title: Git practice app from main story
```

提交：

```bash
git add app.txt
git commit -m "Change title from main story"
```

现在合并同事分支：

```bash
git merge feature/nav-copy-from-anan
git status
```

### 解决冲突

打开 `app.txt`，你会看到类似：

```text
<<<<<<< HEAD
- title: Git practice app from main story
=======
- title: Git practice app from Anan
>>>>>>> feature/nav-copy-from-anan
```

手动改成最终想保留的版本，例如：

```text
- title: Git practice app for real workflows
```

删除所有 `<<<<<<<`、`=======`、`>>>>>>>` 标记，然后：

```bash
git add app.txt
git status
git commit
git log --oneline --graph --decorate -n 8
```

如果只是练习到一半想放弃这次 merge：

```bash
git merge --abort
```

### 检查点

你需要能说出：

- `<<<<<<< HEAD` 一侧是当前分支内容。
- `=======` 到 `>>>>>>> 分支名` 是被合并分支内容。
- 解决冲突后必须 `git add`，表示“这个冲突我处理完了”。

对应课程：`lessons/06-resolve-merge-conflict.md`

## 第七幕：误操作三连

你终于准备继续功能，结果紧张手滑。

### 事件 A：改错文件

你在 `app.txt` 里加了一行临时内容：

```text
- temporary wrong change
```

确认不要后撤销：

```bash
git status
git diff
git restore app.txt
git status
```

### 事件 B：太早 add

你重新加入一行草稿：

```text
- draft help copy
```

然后手滑暂存：

```bash
git add app.txt
git status
```

如果你想取消暂存但保留文件内容：

```bash
git restore --staged app.txt
git status
git diff
```

### 事件 C：commit 信息写得太随意

提交一个小修改：

```bash
git add app.txt
git commit -m "Wip"
git log --oneline -n 3
```

如果这个 commit 还没有推给别人，可以改最近一次提交信息：

```bash
git commit --amend -m "Update help page draft"
git log --oneline -n 3
```

### 检查点

你需要能判断：

- 改错但没暂存：`git restore 文件名`。
- 已暂存但想保留内容：`git restore --staged 文件名`。
- 最近一次 commit 信息写错且未共享：可以 `git commit --amend`。

对应课程：`lessons/07-undo-common-mistakes.md`

## 第八幕：PR 前的历史整理

Reviewer 终于出现：

> “功能看起来可以，但 commit 历史里有 `Wip`、`fix typo`、`fix again`。你能整理一下吗？”

### 你的行动

先看历史：

```bash
git log --oneline --decorate -n 8
git status
```

如果只是最近一次提交信息不好，并且还没有推给别人：

```bash
git commit --amend -m "Update help page copy"
```

如果多个 commit 都属于同一个小目标，PR 前可能会 squash 成一个更清晰的 commit。这个仓库的基础课程只要求你理解目的：

```text
Add help page copy
Fix typo
Fix help wording
```

可以整理成：

```text
Update help page copy
```

如果你还不熟悉 `git rebase -i`，先不要强行操作。可以在 PR 描述里说明这些中间提交的关系，等团队允许时再学习交互式 rebase 或平台的 squash merge。

### 红线

不要随便改这些分支的历史：

- 主分支。
- 发布分支。
- 多个人共同使用的共享分支。
- 已经推给别人并且别人可能基于它继续工作的提交。

### 检查点

你需要能解释：

- `amend` 主要处理最近一次提交。
- `squash` 主要把多个相关 commit 合成一个。
- 改历史前要确认这个分支是不是只有你自己在用。

对应课程：`lessons/08-clean-commit-history.md`

## 终章：发起 PR 前夜

林姐把咖啡放在你桌边：

> “最后一次检查。Git 不要求你不犯错，但要求你知道自己在哪里。”

### PR 前检查清单

```bash
git status
git diff
git diff --staged
git log --oneline --decorate -n 8
git log --oneline --graph --decorate --all -n 10
```

确认：

- 工作区没有意外修改。
- 暂存区没有漏掉或误加内容。
- commit 信息能让 reviewer 看懂目的。
- 分支名能说明任务内容。
- 如果有远端，已经理解当前分支是 ahead、behind 还是 diverged。
- 没有把本地笔记、临时文件、调试垃圾混进提交。
- 没有在共享分支上随意 amend 或 squash。

## 结局判定

### Good End：可发起 PR

你能满足这些条件：

- `git status` 显示干净。
- 你知道这次 PR 改了哪些文件。
- 你知道最近几个 commit 的含义。
- 遇到冲突时能先看 `git status`，再手动解决。
- 你能解释为什么没有随便改共享分支历史。

### Normal End：可以继续练

你完成了大部分操作，但还有一两处靠猜命令完成。建议回到对应 lesson 单独练一次。

### Bad End：需要读档

你不知道当前在哪个分支，也不知道哪些修改已经提交。不要继续乱试，先运行：

```bash
git status
git branch
git log --oneline --decorate -n 8
git stash list
```

把输出读懂后，再决定提交、stash、restore、merge abort，或请同事帮你一起判断。

## 全知识点回收表

- `git status`、工作区、暂存区、提交历史：序章、第一幕、终章。
- `git diff`、`git diff --staged`：序章、第一幕、终章。
- `git stash list`、`git stash show -p`：第二幕、第三幕。
- `git stash apply`、`git stash pop`、`git stash drop`：第二幕、第三幕。
- `git stash push -m`、临时切分支：第二幕、第三幕。
- `git stash -u`、未跟踪文件：第四幕。
- stash 冲突：第三幕。
- `git fetch`、`git pull`、ahead、behind、diverged：第五幕。
- `git switch -c`、功能分支、PR 前准备：第一幕、终章。
- merge 冲突标记与解决：第六幕。
- `git restore`、`git restore --staged`：第七幕。
- `git commit --amend`：第七幕、第八幕。
- `git log --oneline`、`amend`、`squash`、共享分支历史风险：第八幕、终章。
