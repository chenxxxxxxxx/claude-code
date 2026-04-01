# 同步上游仓库代码指南

本项目 fork 自 [claude-code-best/claude-code](https://github.com/claude-code-best/claude-code)，以下说明如何将上游的最新代码同步到你的 fork 仓库。

## 前置条件

- 本地已克隆你的 fork 仓库
- 已配置 git 远程仓库地址

## 操作步骤

### 1. 查看当前远程仓库

```bash
git remote -v
```

确认 `origin` 指向你的 fork 仓库。

### 2. 添加上游仓库

首次同步时，需要添加上游仓库地址（只需执行一次）：

```bash
git remote add upstream https://github.com/claude-code-best/claude-code.git
```

验证是否添加成功：

```bash
git remote -v
```

应看到如下输出：

```
origin    https://github.com/<你的用户名>/claude-code.git (fetch)
origin    https://github.com/<你的用户名>/claude-code.git (push)
upstream  https://github.com/claude-code-best/claude-code.git (fetch)
upstream  https://github.com/claude-code-best/claude-code.git (push)
```

### 3. 拉取上游最新代码

```bash
git fetch upstream
```

### 4. 切换到主分支

```bash
git checkout main
```

### 5. 合并上游代码

```bash
git merge upstream/main
```

### 6. 推送到你的 fork 仓库

```bash
git push origin main
```

## 处理冲突

如果在第 5 步合并时出现冲突，按以下步骤处理：

1. 查看冲突文件：
   ```bash
   git status
   ```

2. 手动编辑冲突文件，解决冲突内容

3. 标记冲突已解决并提交：
   ```bash
   git add <冲突文件>
   git commit
   ```

4. 推送到远程：
   ```bash
   git push origin main
   ```

## 强制覆盖本地修改（谨慎使用）

如果你不需要保留本地的任何修改，想完全与上游保持一致：

```bash
git fetch upstream
git checkout main
git reset --hard upstream/main
git push origin main --force
```

> ⚠️ **警告**：`reset --hard` 和 `push --force` 会永久丢失你的本地修改，请确保你不再需要这些更改。

## 后续同步

首次完成 `upstream` 配置后，以后同步只需重复以下命令：

```bash
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```
