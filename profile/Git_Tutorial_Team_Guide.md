
# Git 教程、协作规范

## 目录
1. [Git 基础知识](#git-基础知识)
2. [Git 常用操作](#git-常用操作)
3. [分支管理与团队协作](#分支管理与团队协作)
4. [团队协作流程](#团队协作流程)
5. [Git 工作流规范](#git-工作流规范)
6. [常见问题与解决方案](#常见问题与解决方案)

---

## Git 基础知识

Git 是一个分布式版本控制系统，用于追踪代码变更，协助团队协作和代码管理。了解 Git 的基本概念有助于有效利用其功能。

- **Repository（仓库）**：项目的文件夹，包括了代码、历史记录等信息。
- **Commit（提交）**：记录一次代码变更，每次提交包含变更的描述。
- **Branch（分支）**：分支是项目的不同版本，在主线之外创建以开发特性或修复问题。
- **Merge（合并）**：将一个分支的更改整合到另一个分支中。

---

## Git 常用操作

### 1. 初始化仓库

```bash
git init
```

创建一个新的 Git 仓库，通常在项目开始时使用。

### 2. 克隆仓库

```bash
git clone <repository-url>
```

从远程仓库克隆代码到本地。

### 3. 配置用户信息

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

配置 Git 用户信息，以便每次提交可以记录作者信息。

### 4. 检查状态

```bash
git status
```

显示当前文件的状态，包括修改、暂存和未跟踪的文件。

### 5. 添加文件到暂存区

```bash
git add <file-name>
git add .
```

将文件添加到暂存区，`git add .` 将添加所有修改的文件。

### 6. 提交更改

```bash
git commit -m "描述此次提交的简要说明"
```

提交更改并为这次更改添加一个简洁描述。

### 7. 查看提交历史

```bash
git log
```

显示所有提交记录。可以使用 `git log --oneline` 来简化输出。

### 8. 创建和切换分支

```bash
git branch <branch-name>
git checkout <branch-name>
```

创建新分支并切换到该分支。

### 9. 查看和删除分支

```bash
git branch -a  # 查看所有分支
git branch -d <branch-name>  # 删除本地分支
git push origin --delete <branch-name>  # 删除远程分支
```

### 10. 配置远程仓库

远程仓库用于团队协作，将本地代码上传到远程仓库让其他人可以获取最新代码。

#### 添加远程仓库
```bash
git remote add aideal <repository-url>
```
为本地仓库添加一个名为 `aideal` 的远程仓库，`<repository-url>` 为远程仓库的地址。

#### 查看远程仓库
```bash
git remote -v
```
查看已添加的远程仓库及其 URL。

#### 修改远程仓库 URL
```bash
git remote set-url aideal <new-repository-url>
```
更改远程仓库的 URL 地址。

#### 删除远程仓库
```bash
git remote remove aideal
```
删除名为 `origin` 的远程仓库配置。

---

### 11. 推送和拉取代码

#### 推送代码到远程仓库
```bash
git push origin <branch-name>
```
将本地分支推送到远程仓库的指定分支。通常用于更新远程仓库的代码。

#### 拉取远程仓库的最新代码
```bash
git pull origin <branch-name>
```
从远程仓库拉取最新的代码并合并到当前分支。

#### 获取远程仓库的更新（不合并）
```bash
git fetch origin
```
获取远程仓库的最新更新，但不会合并到当前分支，可以用于检查远程是否有更新。

---

## 分支管理与团队协作

### 分支命名规范

1. **主分支**：`main` 或 `master`，用于保存稳定的生产代码。
2. **开发分支**：`dev`，用于集成团队的开发代码。
3. **功能分支**：`feature/<feature-name>`，用于开发新功能。
4. **修复分支**：`fix/<issue-name>`，用于修复 Bug。

---

## 团队协作流程

1. **从主仓库拉取最新代码**
    ```bash
    git checkout main
    git pull origin main
    ```

2. **创建新的功能或修复分支**
    ```bash
    git checkout -b feature/<feature-name>
    ```

3. **在分支上开发功能**
    - 频繁提交代码
    - 保持提交信息简洁

4. **完成开发后提交合并请求**
    - 将分支推送到远程仓库
    ```bash
    git push origin feature/<feature-name>
    ```
    - 在 GitHub 上创建合并请求并等待审查。

5. **合并后删除分支**
    - 本地和远程分支均应删除，保持分支清洁。

---

## Git 工作流规范

### 1. 提交规范

- 提交信息应简洁明了，描述清楚更改内容。
- 格式：`<type>(<scope>): <subject>`
- 示例：`feat(user-auth): add login functionality`

#### 提交类型
- `feat`：新增功能
- `fix`：修复 Bug
- `docs`：更新文档
- `style`：代码格式修改，不影响功能
- `refactor`：重构代码
- `test`：增加测试
- `chore`：其他更改

### 2. 分支规范

- 主分支 `main`/`master`：仅用于发布的稳定代码
- 开发分支 `dev`：团队成员合并代码的临时分支
- 功能分支 `feature/`：开发特性时创建，完成后合并到 `dev`
- 修复分支 `fix/`：修复 Bug 后合并到 `dev` 或 `main`

### 3. 合并规范

- 功能开发完成后，合并请求需要至少一个成员审核。
- 合并到主分支 `main` 时，需确保没有冲突。
- 在合并前，建议拉取最新代码并解决冲突。

### 4. 更新本地代码

定期从远程仓库拉取最新代码，确保代码库同步：

```bash
git pull origin <branch-name>
```

---

## 常见问题与解决方案

### 1. 提交信息错误修改

```bash
git commit --amend -m "修改后的提交信息"
```

使用 `--amend` 修正最后一次提交信息。

### 2. 撤销最后一次提交

```bash
git reset --soft HEAD~1
```

撤销提交但保留修改，重新调整代码。

### 3. 回滚到指定提交

```bash
git revert <commit-id>
```

使用 `git revert` 生成新的提交来撤销指定更改。

### 4. 强制推送（请谨慎使用）

```bash
git push -f
```

使用 `-f` 强制推送，通常在修改历史记录时使用，但可能影响其他成员代码。

### 5. 解决冲突

1. 使用 `git status` 查看冲突文件。
2. 手动编辑冲突文件。
3. 添加并提交解决后的文件。

---

## 参考资源

- [Pro Git（中文版）](https://git-scm.com/book/zh/v2) — 官方 Git 指南
- [Atlassian Git 教程](https://www.atlassian.com/git/tutorials) — 简洁易懂的 Git 教程
