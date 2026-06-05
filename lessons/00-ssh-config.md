# 00. SSH 配置

## 生成 SSH

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

## 检查是否有 SSH key

```bash
ls ~/.ssh
```

如果有 `.pub`，说明就已经有 SSH 了。

## 启动 ssh-agent

```bash
eval "$(ssh-agent -s)"
```

## 添加 SSH key

```bash
ssh-add ~/.ssh/id_ed25519
```

## 复制公钥

```bash
cat ~/.ssh/id_ed25519.pub
```

复制：

```text
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAI... rui@example.com
```

## 添加到账号的 Git 中

```text
Settings
  └── SSH and GPG keys
        └── New SSH key
```

## 测试连接

```bash
ssh -T git@github.com
```

## 如果 remote 错了仓库，可以撤回

先查看：

```bash
git remote -v
```

删除：

```bash
git remote remove origin
```

## 同一台机器生成多个 SSH 来使用多个不同的 GitHub 账号

生成 key：

```bash
ssh-keygen -t ed25519 -f ~/.ssh/github_personal -C "personal"
```

将公钥添加到对应的账号 Git：

```text
Settings
→ SSH and GPG Keys
```

配置 SSH config：

```bash
vim ~/.ssh/config
```

内容：

```sshconfig
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/github_personal
```

配置 remote：

```bash
git remote set-url origin \
git@github-personal:Monster-kun/social_nav.git
```
