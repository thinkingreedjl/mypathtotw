# Git 工作流与 GitHub 操作指南：技术写作必备知识
**适用读者**：技术写作新人，需要从零掌握 Git 与 GitHub 基本操作；已有 Git 基础，希望从"单机模式"转向"文档协作模式"的写作者。
---
## 一、安装与基础配置
### （一）安装 Git
- **Windows 系统**：访问 [Git 官方网站](https://git-scm.com/downloads) 下载安装程序，按向导完成安装。
- **macOS 系统**：使用 Homebrew 安装，终端执行 `brew install git`。
- **Linux 系统**：
  - Debian/Ubuntu：`sudo apt-get install git`
  - Red Hat/CentOS：`sudo yum install git`
### （二）基础配置
- 配置用户名：`git config --global user.name "Your Name"`
- 配置用户邮箱：`git config --global user.email "your_email@example.com"`
### （三）配置 SSH Key
**1. 检查是否已有 SSH Key**
执行命令查看是否存在现有密钥，避免重复生成或覆盖：
```bash
ls ~/.ssh
```
若存在 `id_ed25519`/`id_rsa` 等文件，说明已有密钥，可直接使用。
**2. 生成新 SSH Key**
执行命令：
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
- 可直接按回车使用默认存储路径；
- 建议设置 **passphrase** 提升密钥安全性；
- 若设置密码，可通过 `ssh-agent` 或系统钥匙串管理，避免每次验证重复输入。
**3. 复制公钥内容**
```bash
cat ~/.ssh/id_ed25519.pub
```
**4. 添加到 GitHub**
登录 GitHub → Settings → SSH and GPG keys → New SSH key → 粘贴公钥保存。
**5. 验证连接**
```bash
ssh -T git@github.com
```
---
## 二、本地仓库操作
实际工作中，你既可能从本地新建仓库（`git init`），也可能克隆已有仓库（`git clone`），再参与文档写作。
### （一）本地仓库创建
1. 选择工作目录，进入项目文件夹。
2. 初始化仓库：`git init`
### （二）查看状态
- **命令**：`git status`
- **作用**：查看文件修改、暂存、提交状态。
### （三）添加文件到暂存区
- 添加单个文件：`git add user_manual.md`
- 添加所有文件：`git add .`
### （四）提交更改到仓库
- **标准命令**：`git commit -m "提交说明"`
- **文档写作推荐格式**：
```bash
git commit -m "docs: update installation steps in user_manual.md"
```
**说明**：使用 `docs:` 前缀是行业通用约定（Conventional Commits），便于自动生成变更日志，提交信息需说明**修改文档 + 具体内容**。
---
## 三、远程仓库操作
### （一）注册与创建远程仓库
1. 注册 GitHub 账号。
2. 新建仓库：New repository → 填写名称 → 创建。
3. GitHub 新建仓库的默认分支名已从 `master` 改为 `main`，本地分支建议保持一致。
### （二）关联远程仓库并推送
- 关联仓库：`git remote add origin 仓库地址`
- 第一次推送：`git push -u origin main`
- 后续推送：`git push`
### （三）克隆现有仓库
- **作用**：将 GitHub 上的远程仓库完整下载到本地，直接参与写作。
- **SSH 地址（推荐，配合 SSH Key 免密）**：
```bash
git clone git@github.com:用户名/项目名.git
```
- **HTTPS 地址**：
```bash
git clone https://github.com/用户名/项目名.git
```
**说明**：使用 HTTPS 推送时，GitHub 已禁用密码登录，需使用**个人访问令牌（PAT）**作为密码。
### （四）查看远程关联
```bash
git remote -v
```
---
## 四、分支操作
### （一）创建分支
```bash
git branch 分支名
```
### （二）切换分支
```bash
git switch 分支名
```
### （三）创建并切换到新分支（推荐）
```bash
git switch -c 新分支名
```
**说明**：适合写作者：从主分支开出新分支，独立编写/修改文档。
### （四）分支命名建议
分支名应体现修改内容，便于团队识别，例如：
`doc-user-manual`、`fix-install-guide`、`api-reference-update`
### （五）在分支上提交
修改文件 → `git add .` → `git commit -m "docs: 说明内容"`
---
## 五、Pull Request 与代码评审（文档协作核心）
### （一）PR 核心作用
在技术写作团队中，**Pull Request 是文档评审的主要入口**：评审人可逐行查看 Markdown 修改、提出措辞/格式建议，讨论通过后再合并到主分支，保证文档质量与一致性。
### （二）创建 PR 流程
1. 推送本地分支到远程：`git push origin 分支名`
2. 打开 GitHub 仓库，点击 Compare & pull request。
3. 填写标题与修改说明，指派评审人。
4. 点击 Create pull request。
### （三）文档评审
评审人在线评论、建议修改，作者同步更新后再次推送。
### （四）本地拉取 PR 分支（查看效果）
1. 获取远程所有分支信息：`git fetch origin`
2. 基于远程 PR 分支创建本地分支：
```bash
git switch -c 本地分支名 origin/远程PR分支名
```
### （五）合并与删除分支
评审通过 → Merge pull request → 删除远程/本地临时分支。
---
## 六、同步操作与冲突解决
### （一）拉取远程更新
1. 获取更新（不合并）：`git fetch origin`
2. 拉取并合并到本地：`git pull origin main`
### （二）diff 比对（查看修改内容）
- 查看工作区未暂存修改：`git diff`
- 查看暂存区与上次提交差异：`git diff --staged`
- 比对分支差异：`git diff main 分支名`
### （三）撤销与回退（Git 2.23+ 推荐命令）
**1. 撤销工作区修改（未 add）**
```bash
git restore 文件名
```
**2. 撤销暂存区（已 add 未 commit）**
```bash
git restore --staged 文件名
```
**3. 回退本地未推送提交（谨慎使用）**
```bash
git reset --hard HEAD^
```
**4. 安全撤销已推送提交（文档协作推荐）**
```bash
git revert 提交哈希
```
**说明**：`git revert` 不会改写历史，适合公共文档库。
### （四）查看提交日志
```bash
git log
```
### （五）解决冲突
1. 拉取更新时出现冲突，文件会被 Git 标记。
2. 手动编辑文件，删除冲突符号。
3. `git add .` → `git commit -m "docs: resolve conflict in user_manual.md"`
---
## 七、文档场景操作流程
### （一）修改文档
使用 VS Code / Typora 编辑 Markdown 文档。
### （二）提交修改（规范提交信息）
1. `git add user_manual.md`
2. `git commit -m "docs: add v2.0 user manual content"`
常用规范前缀：
- `docs:` 新增/更新文档
- `fix:` 修正错误内容
- `refactor:` 调整结构/格式
**建议**：完成至少 3 次有意义提交后再推送。
### （三）推送修改
```bash
git push origin main
```
### （四）Markdown 写作必备插件（VS Code）
- [Markdown All in One](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one)：目录、快捷键、实时预览
- [Markdown Preview Enhanced](https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced)：高质量渲染、导出 PDF/HTML
- [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)：显示文档每行最后修改人、时间与提交信息，方便追溯变更责任人
---
## 八、仓库结构规范
### （一）标准目录结构
```
tech_writing_project/
├── docs/
│   ├── user_manual.md
│   └── developer_guide.md
├── images/
└── README.md
```
### （二）多语言 / 多版本扩展结构
```
docs/
  en/
    user_manual.md
  zh-CN/
    user_manual.md
```
**说明**：多语言文档按语言代码（en/、zh-CN/）分目录存放。
### （三）README 写作规范
作为技术写作作品集，README 应包含：
- 作者信息与经验
- 项目用途与文档清单
- 贡献说明与使用工具
- 目录导航与快速入口
### （四）.gitignore 文件内容细化
**1. 临时文件**
- Vim 临时文件：`*~`
- VS Code 配置：`.vscode/`
**2. 构建产物**
- 日志：`*.log`
- 构建目录：`build/`
**3. 系统文件**
- Windows：`Thumbs.db`
- macOS：`.DS_Store`
---
## 九、常见问题与排错
**1. Permission denied (publickey)**
检查 SSH Key 是否添加、公钥是否正确、邮箱是否匹配。
**2. 推送要求输入密码**
GitHub 已禁用密码验证，改用 PAT 或 SSH 地址。
**3. git pull 冲突**
按第六章冲突解决步骤处理，手动编辑文件后重新提交。
**4. 提交信息错误**
未推送可用 `git commit --amend` 修改，已推送建议用 `git revert`。
**5. git push 与 git push origin main 的区别**
日常使用完全一样；`git push` 为智能简写，`git push origin main` 为明确指定分支，更安全。
**6. 如何强制推送本地文件**
**安全强制推送（推荐）**：
```bash
git push --force-with-lease origin main
```
**暴力强制推送（慎用）**：
```bash
git push --force origin main
```
**7. 如何把 GitHub 仓库中的 README 取到本地**
执行命令：
```bash
git checkout origin/main -- README.md
```
或拉取全部更新：
```bash
git pull origin main
```
**8. MkDocs 静态网站正确部署流程**
main 分支仅保存源码，网页更新必须执行：
```bash
git add .
git commit -m "docs: 更新内容"
git push origin main
mkdocs gh-deploy --force
```
**9. MkDocs 核心分支说明**
- **main 分支**：存放 Markdown 源码
- **gh-pages 分支**：存放静态网站文件（HTML/CSS/JS）
- GitHub Pages 只会读取 gh-pages 分支内容
**10. 强制推送后网站仍不更新的常见原因**
- 只推送了 main 分支，未执行 `mkdocs gh-deploy --force`
- GitHub Pages 部署源未指向 gh-pages 分支
- 浏览器缓存未刷新（Ctrl+F5）
- GitHub 仍在构建或存在服务器缓存
**11. 一键更新 MkDocs 网站最终命令**
```bash
mkdocs gh-deploy --force
```
---
## 附录：快速参考
### 基础命令速查
| 操作 | 命令 |
|------|------|
| 初始化仓库 | `git init` |
| 克隆仓库 | `git clone <url>` |
| 查看状态 | `git status` |
| 添加文件 | `git add <file>` |
| 提交更改 | `git commit -m "message"` |
| 推送更改 | `git push` |
| 拉取更新 | `git pull` |
| 创建分支 | `git branch <name>` |
| 切换分支 | `git switch <name>` |
| 合并分支 | `git merge <branch>` |
### 提交信息规范
- `docs:` 文档相关
- `fix:` 修复错误
- `feat:` 新增功能
- `refactor:` 重构代码
- `style:` 格式调整
- `test:` 测试相关
- `chore:` 构建/工具相关
---
**文档版本**：1.0  
**最后更新**：2026-03-02  
**适用环境**：Git 2.23+ / GitHub
