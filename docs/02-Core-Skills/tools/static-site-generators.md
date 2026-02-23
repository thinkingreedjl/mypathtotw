# Complete Guide to Generating and Deploying an MkDocs Site to GitHub (Beginner Version)

This guide integrates all operational steps from environment preparation, site construction to GitHub deployment, and summarizes common errors and solutions during the deployment process. It is suitable for beginners to follow directly, enabling them to successfully build and publicly access their own MkDocs site (taking a technical writer learning site as an example).

## Part 1: Complete Operation Process (In Execution Order)

### I. Environment Preparation (Mandatory, Lay a Solid Foundation)

#### 1. Install Python (Recommended Version 3.11 for Best Compatibility)

- Download Link: [Python 3.11.9](https://www.python.org/downloads/release/python-3119/) (Avoid Version 3.13 as some plugins are incompatible)

- Installation Steps:

- Check the box at the bottom of the installation interface labeled 「Add Python 3.11 to PATH」 (Critical step to avoid subsequent command execution failures)

- Click 「Install Now」 and follow the default steps to complete the installation

- Supplementary Note: If executing `python --version` after installation prompts 「not an internal or external command」, reinstall Python and ensure 「Add Python 3.11 to PATH」 is checked; if already installed without checking, you can manually add the Python path to the system environment variables (beginners are advised to reinstall directly for convenience).

Verify Installation: Open CMD (Windows)/Terminal (Mac), enter `python --version`, and if it displays 「Python 3.11.9」, the installation is successful.

#### 2. Install Git (For Version Control, Push Code to GitHub)

- Download Link: [Git Official Download](https://git-scm.com/downloads)

- Installation Steps: Follow the default steps without modifying configurations (Git Bash will be installed automatically, and all subsequent commands will be executed in Git Bash)

- Supplementary Note: If prompted to 「select a default editor」 during installation, beginners can keep the default (Vim) without modification; all subsequent Git-related commands must be executed in Git Bash, not in CMD (to avoid path and command compatibility issues).

- Verify Installation: Open Git Bash, enter `git --version`, and if it displays the Git version number, the installation is successful.

#### 3. Install VS Code (For Writing .md Documents and Configuration Files)

- Download Link: [VS Code Official Download](https://code.visualstudio.com/)

- Installation Steps: Follow the default steps, and you can check 「Add to PATH」

- Essential Plugins (Restart VS Code after installation to take effect):

- Markdown All in One (Facilitates writing .md documents)

- YAML (Facilitates editing mkdocs.yml configuration files and avoids syntax errors)

Supplementary Note: Plugin Installation Method - Open VS Code, click 「Extensions」 (four-square icon) on the left, enter the plugin name in the search box, and click 「Install」; restart VS Code after installation to ensure the plugin takes effect.

#### 4. Install MkDocs and Related Plugins

- Open Git Bash and enter the following commands (execute line by line to ensure network stability):

- Upgrade pip: `python -m pip install --upgrade pip`

- Install MkDocs Core Package: `pip install mkdocs`

- Install Material Theme (Beautiful, Responsive, Suitable for Beginners): `pip install mkdocs-material`

- Install Auxiliary Plugins (Display Update Time, Compress Static Files): `pip install mkdocs-git-revision-date-localized-plugin mkdocs-minify-plugin`

Supplementary Note: If executing the command prompts 「pip is not an internal or external command」, it means Python is not added to the environment variables; reinstall Python and ensure 「Add Python 3.11 to PATH」 is checked. If the network is unstable, you can use a domestic mirror source (such as Alibaba Cloud) and modify the command to `pip install mkdocs -i https://mirrors.aliyun.com/pypi/simple/`; the same applies to other plugin installation commands.

Verify Installation: Enter `mkdocs --version`, and if it displays the MkDocs version number, the installation is successful.

#### 5. GitHub Account Preparation

- Register/Log in to GitHub Account: [GitHub Official Website](https://github.com/)

- Supplementary Note: When registering a GitHub account, the email needs to be verified; the password is recommended to include uppercase and lowercase letters, numbers, and special characters to improve security; you can bind a mobile phone number after logging in to avoid subsequent operation restrictions.

- Create a GitHub Repository (For Storing MkDocs Projects):

- Click the 「+」 in the upper right corner of GitHub → 「New repository」

- Repository Name: Enter a repository name (e.g., 「mkdocs-demo-site」, customizable, recommended to be in English, lowercase, and without spaces)

- Keep other settings default (no need to check 「Add a README file」), click 「Create repository」

- Record the Repository SSH Address (For Subsequent Use): Repository Page → 「Code」 → 「SSH」 → Copy the address (Format: `git@github.com:username/repository-name.git`, Example: `git@github.com:demo-user/mkdocs-demo-site.git`)

### II. Build an MkDocs Local Site

#### 1. Create an MkDocs Project (Locally)

- Open Git Bash and switch to the local directory where you want to store the project (e.g., the mkdocs folder on Drive C):

- Create Directory (Optional): `mkdir /c/mkdocs` (Git Bash Path Format for Windows Systems)

- Switch Directory: `cd /c/mkdocs`

Supplementary Note: If you do not want to place the project on Drive C, you can replace it with another drive (e.g., Drive D), modify the commands to `mkdir /d/mkdocs` and `cd /d/mkdocs`, and update the subsequent paths accordingly; the path separator in Git Bash is 「/」, not the default 「\」 in Windows.

Initialize MkDocs Project: `mkdocs new mkdocs-demo-site` (「mkdocs-demo-site」 is consistent with the GitHub repository name for subsequent convenience, corresponding to the example repository name)

Switch to Project Directory: `cd mkdocs-demo-site` (All subsequent operations will be executed in this directory)

#### 2. Configure the MkDocs Site (Modify mkdocs.yml)

- Open the project directory with VS Code:

- Open VS Code → 「File」 → 「Open Folder」 → Select `C:\mkdocs\mkdocs-demo-site` (Corresponding to the above project directory; if it is Drive D, modify it to `D:\mkdocs\mkdocs-demo-site`)

Edit the mkdocs.yml Configuration File (Core: Replace the default content with the following content to avoid syntax errors):

```yaml
site_name: Technical Writer Guide from Beginner to Pro
theme:
  name: material
  language: en
  palette:
    - scheme: default
      primary: blue
      accent: indigo
      toggle:
        icon: material/weather-sunny
        name: Switch to dark mode
    - scheme: slate
      primary: blue
      accent: indigo
      toggle:
        icon: material/weather-night
        name: Switch to light mode
  features:
    - navigation.tabs
    - navigation.sidebar
    - navigation.sections
    - search.suggest
    - search.highlight
    - toc.integrate
    - content.action.edit
  font:
    text: Roboto
    code: Roboto Mono
  icon:
    repo: fontawesome/brands/github
plugins:
  - git-revision-date-localized:
      type: date
  - minify:
      minify_html: true
```

Supplementary Note: The default mkdocs.yml file only has 1 line `site_name: mkdocs-demo-site`; you need to delete this line and paste the above configuration. After pasting, click 「YAML」 in the lower right corner of VS Code to ensure there are no red wavy lines (no syntax errors).

Configuration Description (No Modification Needed for Beginners): Specify the Material theme, enable common features, load plugins, and ensure there are no YAML syntax errors (add a space after colons, use 2 spaces for indentation).

#### 3. Create Site IA Structure (Organize the docs Folder)

- The docs folder is the core directory for storing site content; organize it according to the following structure (customizable, taking a technical writer learning site as an example):

```plain text
docs/
├─ index.md  # Site Homepage (Mandatory, Default Homepage)
├─ 01-Basics/  # Level 1 Directory (Basics)
│  └─ index.md  # Basics Homepage
├─ 02-Document Types/  # Level 1 Directory (Document Types)
│  └─ index.md
└─ 03-Tool Usage/  # Level 1 Directory (Tool Usage)
   └─ index.md
```

- Supplementary Note: Method to Create Folders/Files - In the 「Explorer」 on the left side of VS Code, right-click 「docs」 → 「New Folder」/「New File」 and name them according to the above structure; it is recommended that file/folder names be in English, without spaces, to avoid deployment errors later; the index.md in each directory is the default homepage and cannot be omitted.

- Write .md Documents: Open the corresponding .md file with VS Code and write content using Markdown syntax (e.g., write the site homepage introduction in index.md and the corresponding learning content in each chapter).

- Supplementary Note: Basic Markdown Syntax (Essential for Beginners): # Level 1 Heading, ## Level 2 Heading, ### Level 3 Heading; **Bold**, *Italic*; [Link Text](Link Address); ![Image Description](Image Path); Beginners can first write simple content (e.g., enter 「# Homepage」 and 「Welcome to My MkDocs Site」) and gradually improve it after deployment.

#### 4. Preview the Site Locally (Verify Effects)

- Enter the command in Git Bash (in the project directory): `mkdocs serve`

- Supplementary Note: Before executing the command, ensure that the current path of Git Bash is the project directory (the prompt displays 「xxx MINGW64 /c/mkdocs/mkdocs-demo-site」); if the path is incorrect, execute `cd /c/mkdocs/mkdocs-demo-site` to switch.

- Preview Success: The terminal prompts 「Serving on http://127.0.0.1:8000」; open a browser and visit this address to see the real-time effect of the site.

- Supplementary Note: If the browser cannot access it, check the terminal for error prompts (refer to Part 2 for common problem troubleshooting); when modifying .md files or mkdocs.yml during preview, the browser will refresh automatically, and there is no need to re-execute `mkdocs serve`.

- Exit Preview: Press 「Ctrl+C」 on the keyboard to stop the local service.

### III. Initialize the Local Git Repository

- Execute the following commands in Git Bash (in the project directory) to bring the local project under Git version control:

- Initialize Git Repository: `git init` (Prompt 「Initialized empty Git repository in...」 indicates success, and a hidden .git folder will be generated)

- Add All Files to the Staging Area: `git add --all` (No output indicates success)

- Commit Files to the Local Repository: `git commit -m "Initial commit: Add MkDocs config and docs structure"` (The commit description can be customized for clarity)

- Rename the Local Branch to main (Adapt to GitHub's Default Branch): `git branch -M main`

Supplementary Note: If executing `git commit` prompts 「Please tell me who you are」, it means Git user information is not configured; execute the following commands to configure (replace with your own GitHub email and username): `git config --global user.email "your-github-email@example.com"` and `git config --global user.name "your-github-username"`, then re-execute the commit command after configuration.

Verify Commit: Enter `git log`; if you can see the commit record, it is successful.

### IV. Configure SSH Protocol (Solve HTTPS Connection Reset Issues)

#### 1. Generate SSH Keys (Locally)

- Execute the command in Git Bash (replace with your own GitHub registered email): `ssh-keygen -t ed25519 -C "your-github-email@example.com"`

- Press the Enter key throughout the process (no need to modify the key path or set a password):

- Prompt 「Enter file in which to save the key」 → Press Enter (Default Path: `~/.ssh/id_ed25519`)

- Prompt 「Enter passphrase」 → Press Enter (No password set for simplified operation)

Verify Key Generation: Enter `ls ~/.ssh/`; if you can see 「id_ed25519」 (private key) and 「id_ed25519.pub」 (public key), it is successful.

#### 2. Add the SSH Public Key to GitHub (For Authentication)

- Copy the Local Public Key Content (Execute in Git Bash): `clip < ~/.ssh/id_ed25519.pub` (Automatically copied to the clipboard, no output)

- Supplementary Note: If the `clip` command has no response (Mac system), you can execute `cat ~/.ssh/id_ed25519.pub` and manually copy the complete public key content displayed (do not miss any characters).

- Log in to GitHub and Add the Public Key:

- Upper Right Corner Avatar → 「Settings」 → Left Side 「SSH and GPG keys」 → 「New SSH key」

- Title: Enter any name (e.g., 「My Windows PC」 for easy identification, customizable)

- Key type: Select 「Authentication key」

- Key: Paste the public key content from the clipboard (Ensure it is a complete single-line string without line breaks or extra spaces)

- Click 「Add SSH key」 and enter your GitHub password for verification.

#### 3. Verify SSH Connection (Critical Step)

- Execute the command in Git Bash: `ssh -T git@github.com`

- First Execution Prompt 「Are you sure you want to continue connecting」 → Enter 「yes」 (lowercase) and press Enter

- Verification Success: Displays 「Hi your-github-username! You've successfully authenticated, but GitHub does not provide shell access.」 (Replace your-github-username with your own username)

#### 4. Configure the SSH Remote Address of the Local Repository

- Execute the command in Git Bash (in the project directory) (replace with your own GitHub repository SSH address, Example: `git@github.com:demo-user/mkdocs-demo-site.git`):

- Delete the Old HTTPS Address (If Any): `git remote remove origin`

- Add the SSH Remote Address: `git remote add origin git@github.com:demo-user/mkdocs-demo-site.git`

Verify Configuration: Enter `git remote -v`; if it displays the SSH format address, it is successful.

### V. Push the Local Project to GitHub

- Execute the push command in Git Bash (in the project directory): `git push -u origin main`

- Supplementary Note: The first push may have a delay; please wait patiently for 10-30 seconds. If the push prompts 「failed to push some refs」, execute `git pull --rebase origin main` (pull remote repository content and merge conflicts), then re-execute the push command.

- Push Success: The terminal displays content such as 「Branch 'main' set up to track remote branch 'main' from 'origin'」

- Verify Push: Open the GitHub repository page; after refreshing, you can see project files such as mkdocs.yml and the docs folder, which indicates success.

### VI. Configure GitHub Pages (Enable Public Site Access)

#### 1. Create GitHub Actions Automatic Deployment Configuration

- Open the GitHub Repository Page → 「Actions」 → 「New workflow」

- Scroll to the bottom of the page and click 「set up a workflow yourself」

- Delete the default code and paste the following configuration (for automatic deployment of the MkDocs site):

```yaml
name: Deploy MkDocs to GitHub Pages

on:
  push:
    branches: [ main ]  # Trigger deployment when pushing to the main branch

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        with:
          fetch-depth: 0  # Pull all commit records (for the git-revision-date plugin)

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.11"  # Python version compatible with local

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install mkdocs-material mkdocs-git-revision-date-localized-plugin mkdocs-minify-plugin

      - name: Build MkDocs site
        run: mkdocs build

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./site  # MkDocs build output directory
```

- Supplementary Note: When pasting the configuration, ensure the code is complete and without extra spaces; if you are worried about pasting errors, you can directly copy the configuration code in this document to avoid manual input errors.

- Enter Commit message: `Add MkDocs deploy workflow`, click 「Commit changes」

#### 2. Enable GitHub Pages

- GitHub Repository → 「Settings」 → Left Side 「Pages」

- In 「Build and deployment」 → 「Source」, select 「GitHub Actions」

- After saving, wait 1-2 minutes (Actions will automatically build and deploy)

- Supplementary Note: If Actions deployment fails, click the repository → 「Actions」, check the 「Steps」 of the failure record, and troubleshoot with reference to Q12 in Part 2; a green checkmark will be displayed after successful build.

#### 3. Obtain the Public Access Link

- Refresh the GitHub Pages page, and a green prompt will appear: 「Your site is live at https://your-github-username.github.io/repository-name/」 (Example: `https://demo-user.github.io/mkdocs-demo-site/`)

- Supplementary Note: It may take 5-10 minutes for the site to take effect (GitHub Pages cache); if it cannot be accessed after refreshing, wait a few minutes and try again; if it still cannot be accessed, check if Actions has built successfully and if the repository name is correct.

- Copy this link to share your MkDocs site with others.

## Part 2: Common Questions FQA (Errors and Solutions Encountered Throughout the Process)

The following are all possible errors encountered during the entire deployment process, arranged in the order of occurrence. Each question corresponds to a specific solution, which beginners can directly refer to for troubleshooting.

### Q1: When executing mkdocs serve, a warning is prompted for the git-revision-date-localized plugin (no .git folder)

#### Error Prompt

Warning: git-revision-date-localized plugin could not find a git repository

#### Solution

Reason: The local project has not initialized a Git repository, so the plugin cannot read commit records.

Execute the following commands in the project directory:

```bash
git init  # Initialize Git repository
git add --all  # Add all files
git commit -m "Initial commit"  # Commit files
```

Re-execute `mkdocs serve`, and the warning will disappear.

### Q2: When executing mkdocs serve, a Traceback error occurs (configuration file syntax error)

#### Error Prompt

Traceback (most recent call last): ... File "xxx/mkdocs/config/base.py", line 197, in load_config raise ConfigError(f"Error loading configuration file: {e}")

#### Solution

Reason: There is a YAML syntax error in the mkdocs.yml configuration file (Common Errors: No space after colon, messy indentation, special characters not quoted).

1. Execute the command to troubleshoot specific errors: `mkdocs build --strict`; the terminal will display the error line and reason;

2. Key Correction Points:

- A space must be added after the colon `:` of all key-value pairs (e.g., `theme: material` instead of `theme:material`);

- Indentation must use 2 spaces uniformly; do not mix Tabs and spaces;

- Strings containing special characters such as `:`, `#`, and & must be quoted (e.g., `link: "https://github.com/xxx?a=1&b=2"`).

### Q3: When executing mkdocs serve, TemplateNotFound: '.icons/material/pen-nib.svg' is prompted

#### Error Prompt

jinja2.exceptions.TemplateNotFound: '.icons/material/pen-nib.svg' not found in search paths: ...

#### Solution

Reason: The Material theme version is incompatible with the icon name, or the theme installation is incomplete.

Option 1 (Fastest): Delete the custom logo configuration in mkdocs.yml and comment/delete the following line:

```yaml
# logo: material/pen-nib  # Comment this line to use the default logo
```

Option 2 (Keep Custom Logo): Reinstall a stable version of the Material theme and replace the icon name:

```bash
pip uninstall -y mkdocs-material
pip install mkdocs-material==9.5.22  # Stable version
```

Modify the logo configuration in mkdocs.yml to: `logo: material/pencil` (Compatible with all versions).

### Q4: When executing git commit, nothing to commit, working tree clean is prompted

#### Error Prompt

On branch master nothing to commit, working tree clean

#### Solution

Reason: Files are not added to the Git staging area, or not in the project directory, or the branch name does not match.

1. Confirm you are in the project directory: `cd /c/mkdocs/mkdocs-demo-site` (Corresponding to your own project directory);

2. Force add all files: `git add --all`;

3. Re-commit: `git commit -m "Initial commit: Add MkDocs config and docs structure"`;

4. Rename the branch to main: `git branch -M main`.

### Q5: When executing git push -u origin main, Connection was reset is prompted

#### Error Prompt

fatal: unable to access 'https://github.com/demo-user/mkdocs-demo-site.git/': Recv failure: Connection was reset

#### Solution

Reason: The HTTPS protocol connection is unstable and is blocked by a firewall/proxy.

Core Solution: Use the SSH protocol for pushing (Refer to Part 1 「IV. Configure SSH Protocol」), Steps:

- Generate SSH keys and add them to GitHub;

- Configure the SSH remote address of the local repository;

- Re-execute `git push -u origin main`.

Auxiliary Troubleshooting: Turn off proxies, firewalls/anti-virus software, and test with mobile hotspots.

### Q6: Git Bash prompts demo-user@DESKTOP-XXXXXX MINGW64 ~, and I don't know the next step

#### Error/Prompt Description

This is not an error, but a normal command prompt of Git Bash, indicating that you are currently in the user's home directory (`C:\Users\demo-user`, demo-user is an example username, XXXXXX is an example computer name), and the terminal is in a standby state.

#### Solution

Switch to the MkDocs project directory and continue executing subsequent commands:

```bash
cd /c/mkdocs/mkdocs-demo-site  # Switch to the project directory
```

After switching, the prompt will display the project path, and you can execute subsequent Git/MkDocs commands.

### Q7: When executing git push, The authenticity of host 'github.com (::1)' can't be established is prompted

#### Error Prompt

The authenticity of host 'github.com (::1)' can't be established. ED25519 key fingerprint is: SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU Are you sure you want to continue connecting (yes/no/[fingerprint])?

#### Solution

Reason: When connecting to GitHub via SSH for the first time, Git needs to verify the server's authenticity.

Enter **yes** (lowercase) and press Enter after the prompt (do not enter Y or YES); subsequent connections will not prompt again.

### Q8: When executing ssh-add ~/.ssh/id_ed25519, No such file or directory is prompted

#### Error Prompt

/c/Users/demo-user/.ssh/id_ed25519: No such file or directory (demo-user is an example username)

#### Solution

Reason: No SSH key is generated locally, or the key path/filename is incorrect.

1. Check the .ssh folder: `ls ~/.ssh/` to confirm there is no id_ed25519 file;

2. Re-generate the key (Press Enter throughout the process):

```bash
ssh-keygen -t ed25519 -C "your-github-email@example.com"
```

3. Verify Generation: `ls ~/.ssh/`; if you can see id_ed25519 and id_ed25519.pub, it is successful.

### Q9: When executing ssh -T git@github.com, Permission denied (publickey) is prompted

#### Error Prompt

git@github.com: Permission denied (publickey).

#### Solution

Reason: The SSH public key is not correctly added to GitHub, or the local SSH agent has not loaded the private key.

Option 1: Restart the SSH agent and load the private key (Mandatory for Windows):

```bash
ssh-agent -k  # Terminate the old agent
eval "$(ssh-agent -s)"  # Restart the agent
ssh-add ~/.ssh/id_ed25519  # Load the private key
```

Option 2: Check the consistency between the local public key and the GitHub public key:

```bash
cat ~/.ssh/id_ed25519.pub  # View the local public key
```

Log in to GitHub → SSH and GPG keys, compare the public key content to ensure they are completely consistent (no omissions or extra spaces); re-add if inconsistent.

Option 3: Use RSA Key (Alternative Solution):

```bash
ssh-keygen -t rsa -b 4096 -C "your-github-email@example.com"  # Generate RSA key
clip < ~/.ssh/id_rsa.pub  # Copy the public key to GitHub
ssh-add ~/.ssh/id_rsa  # Load the private key
```

### Q10: When adding an SSH public key to GitHub, Key is invalid. You must supply a key in OpenSSH public key format is prompted

#### Error Prompt

Key is invalid. You must supply a key in OpenSSH public key format

#### Solution

Reason: The pasted public key does not conform to the OpenSSH format (wrong file copied, incomplete content, extra line breaks).

1. Re-copy the correct public key (Ensure it is a public key file with the .pub suffix):

```bash
clip < ~/.ssh/id_ed25519.pub  # ED25519 key
# Or clip < ~/.ssh/id_rsa.pub  # RSA key
```

2. When pasting to GitHub, ensure it is a 「complete single-line string」 without line breaks or extra spaces;

3. Alternative Solution: Force generate an OpenSSH format key:

```bash
ssh-keygen -t ed25519 -C "your-github-email@example.com" -m PEM  # Force OpenSSH format
```

### Q11: When executing ssh -T git@github.com, Hi demo-user! You've successfully authenticated, but GitHub does not provide shell access. is displayed

#### Prompt Description

This is not an error, but a prompt for successful SSH authentication! It means GitHub has confirmed your identity (demo-user is an example username), and you can normally execute Git push operations.

#### Next Step

Switch to the project directory and execute the push command:

```bash
cd /c/mkdocs/mkdocs-demo-site
git push -u origin main
```

### Q12: GitHub Actions Deployment Failed

#### Error/Prompt Description

A red cross is displayed on the GitHub Actions page, and the deployment fails.

#### Solution

Reason: Actions configuration error, incompatible Python version, or failed dependency installation.

1. Click the failed Actions record and check the 「Steps」 of the error prompt;

2. Common Correction Points:

- Ensure the Python version in the Actions configuration is 3.11 (consistent with the local version);

- Re-commit the Actions configuration file to ensure there are no syntax errors;

- If dependency installation fails, re-execute the relevant `pip install` command locally, verify it is correct, and then push.

### Q13: Local Preview is Normal, but GitHub Pages Access Displays 404 Error

#### Error/Prompt Description

When accessing the GitHub Pages link with a browser, 「404 Not Found」 is displayed.

#### Solution

Reason: GitHub Pages is not correctly pointing to the build output directory, or Actions has not built successfully.

1. Check the Actions build status: Repository → 「Actions」, ensure the latest build is a green checkmark; if it fails, troubleshoot with reference to Q12;

2. Check the GitHub Pages configuration: Repository → 「Settings」 → 「Pages」, confirm 「Source」 is 「GitHub Actions」 and there are no other incorrect configurations;

3. Wait Patiently: It may take 5-10 minutes for GitHub Pages to take effect; refresh the browser and try again;

4. Verify Repository Name: Ensure the repository name in the access link is completely consistent with the GitHub repository name (case-sensitive).

### Supplementary Notes

All operations are based on the Windows system (Git Bash); for Mac/Linux systems, the path format can be replaced (e.g., `C:/mkdocs` in Windows is replaced with `/Users/username/mkdocs` in Mac), and the commands are completely consistent. For beginners, it is recommended to execute commands line by line and not skip any steps. If you encounter an error not listed in the FQA section, first check the terminal error prompt carefully—most errors will clearly indicate the cause (such as missing files, syntax errors, or network issues). You can also copy the error prompt to search for solutions online, as most common MkDocs deployment issues have been discussed and resolved by the developer community.

After successful deployment, if you need to update the site content (such as modifying .md documents or adjusting the mkdocs.yml configuration), you only need to complete the following simple steps: 1. Edit the corresponding files in VS Code; 2. Execute `git add --all` and `git commit -m "Update website content: [brief description of changes]"` in Git Bash to commit local modifications; 3. Execute `git push -u origin main` to push the modifications to GitHub. GitHub Actions will automatically trigger a new build and deployment, and the updated content will take effect on the public site within 5-10 minutes (subject to GitHub cache).

It is important to note that the repository name and project directory name should remain consistent throughout the operation to avoid path confusion and deployment failures. In addition, it is recommended to regularly back up local project files, especially the mkdocs.yml configuration file and important .md documents, to prevent data loss due to accidental deletion or system errors. For beginners, it is not recommended to modify the default configurations of MkDocs and related plugins without guidance—you can gradually explore and optimize the site style and functions after becoming familiar with the basic operation process.

Finally, if you want to customize the site domain name (replace the default `https://your-github-username.github.io/repository-name/` with your own domain), you can refer to GitHub's official documentation for GitHub Pages domain configuration. This step is optional and can be implemented after you have fully mastered the basic deployment process.
> (Note: Some parts of this document may be generated by AI.)



# MkDocs站点部署到GitHub完整指南（初学者版）

本文整合了从环境准备、站点搭建到GitHub部署的全部操作步骤，并汇总了部署过程中常见的错误及解决方案，适合初学者直接跟随操作，可成功搭建并公开访问自己的MkDocs站点（以技术文档工程师学习站点为例）。

## 第一部分：完整操作流程（按执行顺序）

### 一、环境准备（必做，打好基础）

#### 1. 安装Python（推荐3.11版本，兼容性最佳）

- 下载链接：[Python 3.11.9](https://www.python.org/downloads/release/python-3119/)（避免3.13版本，部分插件不兼容）

- 安装步骤：

- 勾选安装界面底部的「Add Python 3.11 to PATH」（关键步骤，避免后续命令执行失败）

- 点击「Install Now」，跟随默认步骤完成安装即可

- 补充说明：若安装后执行`python --version`提示「不是内部或外部命令」，需重新安装Python并确保勾选「Add Python 3.11 to PATH」；若已安装未勾选，可手动将Python路径添加到系统环境变量（初学者建议直接重新安装，更便捷）。

验证安装：打开CMD（Windows）/终端（Mac），输入`python --version`，若显示「Python 3.11.9」则安装成功

#### 2. 安装Git（用于版本控制，将代码推送到GitHub）

- 下载链接：[Git官方下载](https://git-scm.com/downloads)

- 安装步骤：跟随默认步骤，无需修改配置（会自动安装Git Bash，后续所有命令均在Git Bash中执行）

- 补充说明：安装过程中若出现「选择默认编辑器」，初学者保持默认（Vim）即可，无需修改；后续所有Git相关命令，均在Git Bash中执行，不要在CMD中执行（避免路径和命令兼容性问题）。

- 验证安装：打开Git Bash，输入`git --version`，若显示Git版本号则安装成功

#### 3. 安装VS Code（用于编写.md文档和配置文件）

- 下载链接：[VS Code官方下载](https://code.visualstudio.com/)

- 安装步骤：跟随默认步骤，可勾选「Add to PATH」

- 必备插件（安装后重启VS Code生效）：

- Markdown All in One（便捷编写.md文档）

- YAML（便捷编辑mkdocs.yml配置文件，避免语法错误）

补充说明：插件安装方法——打开VS Code，点击左侧「扩展」（四个方块图标），在搜索框输入插件名称，点击「安装」；安装完成后重启VS Code，确保插件生效。

#### 4. 安装MkDocs及相关插件

- 打开Git Bash，输入以下命令（逐行执行，确保网络稳定）：

- 升级pip：`python -m pip install --upgrade pip`

- 安装MkDocs核心包：`pip install mkdocs`

- 安装Material主题（美观、响应式，适合初学者）：`pip install mkdocs-material`

- 安装辅助插件（显示更新时间、压缩静态文件）：`pip install mkdocs-git-revision-date-localized-plugin mkdocs-minify-plugin`

补充说明：若执行命令提示「pip不是内部或外部命令」，说明Python未添加到环境变量，重新安装Python并勾选「Add Python 3.11 to PATH」；若网络不稳定，可使用国内镜像源（如阿里云），将命令修改为`pip install mkdocs -i https://mirrors.aliyun.com/pypi/simple/`，其他插件安装命令同理。

验证安装：输入`mkdocs --version`，若显示MkDocs版本号则安装成功

#### 5. GitHub账号准备

- 注册/登录GitHub账号：[GitHub官方网站](https://github.com/)

- 补充说明：注册GitHub账号时，邮箱需验证；密码建议包含大小写字母、数字和特殊字符，提升安全性；登录后可绑定手机号，避免后续操作受限。

- 创建GitHub仓库（用于存放MkDocs项目）：

- 点击GitHub右上角「+」→「New repository」

- 仓库名称：输入仓库名称（例如「mkdocs-demo-site」，可自定义，建议英文、小写、无空格）

- 其他设置保持默认（无需勾选「Add a README file」），点击「Create repository」

- 记录仓库SSH地址（后续使用）：仓库页面→「Code」→「SSH」→复制地址（格式：`git@github.com:用户名/仓库名.git`，示例：`git@github.com:demo-user/mkdocs-demo-site.git`）

### 二、搭建MkDocs本地站点

#### 1. 创建MkDocs项目（本地）

- 打开Git Bash，切换到本地想要存放项目的目录（例如C盘mkdocs文件夹）：

- 创建目录（可选）：`mkdir /c/mkdocs`（Windows系统Git Bash路径格式）

- 切换目录：`cd /c/mkdocs`

补充说明：若不想将项目放在C盘，可更换为其他磁盘（如D盘），命令改为`mkdir /d/mkdocs`、`cd /d/mkdocs`，后续路径同步修改即可；Git Bash中路径分隔符为「/」，而非Windows默认的「\」。

初始化MkDocs项目：`mkdocs new mkdocs-demo-site`（「mkdocs-demo-site」与GitHub仓库名称一致，方便后续操作，对应示例仓库名称）

切换到项目目录：`cd mkdocs-demo-site`（后续所有操作均在此目录下执行）

#### 2. 配置MkDocs站点（修改mkdocs.yml）

- 用VS Code打开项目目录：

- 打开VS Code→「文件」→「打开文件夹」→选择`C:\mkdocs\mkdocs-demo-site`（对应上述项目目录；若为D盘，改为`D:\mkdocs\mkdocs-demo-site`）

编辑mkdocs.yml配置文件（核心：复制以下内容替换默认内容，避免语法错误）：

```yaml
site_name: 技术文档工程师从入门到精通
theme:
  name: material
  language: zh
  palette:
    - scheme: default
      primary: blue
      accent: indigo
      toggle:
        icon: material/weather-sunny
        name: 切换到深色模式
    - scheme: slate
      primary: blue
      accent: indigo
      toggle:
        icon: material/weather-night
        name: 切换到浅色模式
  features:
    - navigation.tabs
    - navigation.sidebar
    - navigation.sections
    - search.suggest
    - search.highlight
    - toc.integrate
    - content.action.edit
  font:
    text: Roboto
    code: Roboto Mono
  icon:
    repo: fontawesome/brands/github
plugins:
  - git-revision-date-localized:
      type: date
  - minify:
      minify_html: true
```

补充说明：默认mkdocs.yml文件仅1行`site_name: mkdocs-demo-site`，需删除该行并粘贴上述配置；粘贴后点击VS Code右下角「YAML」，确保无红色波浪线（无语法错误）。

配置说明（初学者无需修改）：指定Material主题、开启常用功能、加载插件，确保无YAML语法错误（冒号后加空格、缩进用2个空格）。

#### 3. 创建站点IA结构（整理docs文件夹）

- docs文件夹是存放站点内容的核心目录，按以下结构整理（可自定义，以技术文档工程师学习站点为例）：

```plain text
docs/
├─ index.md  # 站点首页（必选，默认首页）
├─ 01-基础入门/  # 一级目录（基础入门）
│  └─ index.md  # 基础入门首页
├─ 02-文档类型/  # 一级目录（文档类型）
│  └─ index.md
└─ 03-工具使用/  # 一级目录（工具使用）
   └─ index.md
```

- 补充说明：创建文件夹/文件方法——在VS Code左侧「资源管理器」中，右键点击「docs」→「新建文件夹」/「新建文件」，按上述结构命名；建议文件/文件夹名称用英文、无空格，避免后续部署出错；每个目录的index.md是默认首页，不可省略。

- 编写.md文档：用VS Code打开对应.md文件，使用Markdown语法编写内容（例如在index.md中编写站点首页介绍，在各章节中编写对应学习内容）。

- 补充说明：基础Markdown语法（初学者必备）：# 一级标题、## 二级标题、### 三级标题；**加粗**、*斜体*；[链接文本](链接地址)；![图片描述](图片路径)；初学者可先编写简单内容（如输入「# 首页」「欢迎访问我的MkDocs站点」），部署完成后再逐步完善。

#### 4. 本地预览站点（验证效果）

- 在Git Bash中（项目目录下）输入命令：`mkdocs serve`

- 补充说明：执行命令前，确保Git Bash当前路径是项目目录（提示符显示「xxx MINGW64 /c/mkdocs/mkdocs-demo-site」）；若路径错误，执行`cd /c/mkdocs/mkdocs-demo-site`切换。

- 预览成功：终端提示「Serving on http://127.0.0.1:8000」，打开浏览器访问该地址，即可看到站点实时效果

- 补充说明：若浏览器无法访问，查看终端是否有错误提示（参考第二部分常见问题排查）；预览时修改.md文件或mkdocs.yml，浏览器会自动刷新，无需重新执行`mkdocs serve`。

- 退出预览：键盘按「Ctrl+C」，停止本地服务

### 三、初始化本地Git仓库

- 在Git Bash中（项目目录下）执行以下命令，将本地项目纳入Git版本控制：

- 初始化Git仓库：`git init`（提示「Initialized empty Git repository in...」即为成功，会生成隐藏的.git文件夹）

- 将所有文件添加到暂存区：`git add --all`（无输出即为成功）

- 将文件提交到本地仓库：`git commit -m "Initial commit: Add MkDocs config and docs structure"`（提交描述可自定义，清晰即可）

- 将本地分支重命名为main（适配GitHub默认分支）：`git branch -M main`

补充说明：若执行`git commit`提示「Please tell me who you are」，说明未配置Git用户信息，执行以下命令配置（替换为自己的GitHub邮箱和用户名）：`git config --global user.email "你的GitHub邮箱@example.com"`、`git config --global user.name "你的GitHub用户名"`，配置完成后重新执行提交命令。

验证提交：输入`git log`，若能看到提交记录即为成功

### 四、配置SSH协议（解决HTTPS连接重置问题）

#### 1. 生成SSH密钥（本地）

- 在Git Bash中执行命令（替换为自己的GitHub注册邮箱）：`ssh-keygen -t ed25519 -C "你的GitHub邮箱@example.com"`

- 全程按回车键（无需修改密钥路径、无需设置密码）：

- 提示「Enter file in which to save the key」→ 按回车（默认路径：`~/.ssh/id_ed25519`）

- 提示「Enter passphrase」→ 按回车（不设置密码，简化操作）

验证密钥生成：输入`ls ~/.ssh/`，若能看到「id_ed25519」（私钥）和「id_ed25519.pub」（公钥）即为成功

#### 2. 将SSH公钥添加到GitHub（用于身份验证）

- 复制本地公钥内容（Git Bash中执行）：`clip < ~/.ssh/id_ed25519.pub`（自动复制到剪贴板，无输出）

- 补充说明：若执行`clip`命令无响应（Mac系统），可执行`cat ~/.ssh/id_ed25519.pub`，手动复制输出的完整公钥内容（不要遗漏任何字符）。

- 登录GitHub，添加公钥：

- 右上角头像→「Settings」→左侧「SSH and GPG keys」→「New SSH key」

- Title：输入任意名称（例如「My Windows PC」，方便识别，可自定义）

- Key type：选择「Authentication key」

- Key：粘贴剪贴板中的公钥内容（确保是完整的单行字符串，无换行、无多余空格）

- 点击「Add SSH key」，输入GitHub密码验证即可

#### 3. 验证SSH连接（关键步骤）

- 在Git Bash中执行命令：`ssh -T git@github.com`

- 首次执行提示「Are you sure you want to continue connecting」→ 输入「yes」（小写）并按回车

- 验证成功：显示「Hi 你的GitHub用户名! You've successfully authenticated, but GitHub does not provide shell access.」（将你的GitHub用户名替换为自己的用户名）

#### 4. 配置本地仓库的SSH远程地址

- 在Git Bash中（项目目录下）执行命令（替换为自己的GitHub仓库SSH地址，示例：`git@github.com:demo-user/mkdocs-demo-site.git`）：

- 删除旧的HTTPS地址（若有）：`git remote remove origin`

- 添加SSH远程地址：`git remote add origin git@github.com:demo-user/mkdocs-demo-site.git`

验证配置：输入`git remote -v`，若显示SSH格式地址即为成功

### 五、将本地项目推送到GitHub

- 在Git Bash中（项目目录下）执行推送命令：`git push -u origin main`

- 补充说明：首次推送可能有延迟，请耐心等待10-30秒；若推送提示「failed to push some refs」，执行`git pull --rebase origin main`（拉取远程仓库内容并合并冲突），再重新执行推送命令。

- 推送成功：终端显示「Branch 'main' set up to track remote branch 'main' from 'origin'」等内容

- 验证推送：打开GitHub仓库页面，刷新后能看到mkdocs.yml、docs文件夹等项目文件即为成功

### 六、配置GitHub Pages（实现站点公开访问）

#### 1. 创建GitHub Actions自动部署配置

- 打开GitHub仓库页面→「Actions」→「New workflow」

- 滚动到页面底部，点击「set up a workflow yourself」

- 删除默认代码，粘贴以下配置（用于自动部署MkDocs站点）：

```yaml
name: Deploy MkDocs to GitHub Pages

on:
  push:
    branches: [ main ]  # 推送到main分支时触发部署

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
        with:
          fetch-depth: 0  # 拉取所有提交记录（用于git-revision-date插件）

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: "3.11"  # 与本地兼容的Python版本

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install mkdocs-material mkdocs-git-revision-date-localized-plugin mkdocs-minify-plugin

      - name: Build MkDocs site
        run: mkdocs build

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./site  # MkDocs构建产物目录
```

- 补充说明：粘贴配置时，确保代码完整、无多余空格；若担心粘贴错误，可直接复制本文档中的配置代码，避免手动输入出错。

- 输入Commit message：`Add MkDocs deploy workflow`，点击「Commit changes」

#### 2. 启用GitHub Pages

- GitHub仓库→「Settings」→左侧「Pages」

- 在「Build and deployment」→「Source」中，选择「GitHub Actions」

- 保存后，等待1-2分钟（Actions会自动构建部署）

- 补充说明：若Actions构建失败，点击仓库→「Actions」，查看失败记录的「Steps」，参考第二部分Q12排查；构建成功后会显示绿色对勾。

#### 3. 获取公开访问链接

- 刷新GitHub Pages页面，会出现绿色提示：「Your site is live at https://你的GitHub用户名.github.io/仓库名/」（示例：`https://demo-user.github.io/mkdocs-demo-site/`）

- 补充说明：站点生效可能需要5-10分钟（GitHub Pages缓存）；刷新后无法访问，可耐心等待几分钟再尝试；若仍无法访问，检查Actions是否构建成功、仓库名称是否正确。

- 复制该链接，即可分享给他人访问你的MkDocs站点

## 第二部分：常见问题FQA（全程遇到的错误及解决方案）

以下是部署全程可能遇到的所有错误，按出现顺序排列，每个问题对应具体解决方案，初学者可直接参考排查。

### Q1：执行mkdocs serve时，提示git-revision-date-localized插件警告（无.git文件夹）

#### 错误提示

Warning: git-revision-date-localized plugin could not find a git repository

#### 解决方案

原因：本地项目未初始化Git仓库，插件无法读取提交记录。

在项目目录下执行以下命令：

```bash
git init  # 初始化Git仓库
git add --all  # 添加所有文件
git commit -m "Initial commit"  # 提交文件
```

重新执行`mkdocs serve`，警告即可消失。

### Q2：执行mkdocs serve时，出现Traceback错误（配置文件语法错误）

#### 错误提示

Traceback (most recent call last): ... File "xxx/mkdocs/config/base.py", line 197, in load_config raise ConfigError(f"Error loading configuration file: {e}")

#### 解决方案

原因：mkdocs.yml配置文件存在YAML语法错误（高频错误：冒号后无空格、缩进混乱、特殊字符未加引号）。

1. 执行命令排查具体错误：`mkdocs build --strict`，终端会显示错误行及原因；

2. 关键修正点：

- 所有键值对的冒号`:`后必须加空格（例如`theme: material`，而非`theme:material`）；

- 缩进必须统一使用2个空格，不要混合使用Tab和空格；

- 包含`:`、`#`、&等特殊字符的字符串，必须加引号（例如`link: "https://github.com/xxx?a=1&b=2"`）。

### Q3：执行mkdocs serve时，提示TemplateNotFound: '.icons/material/pen-nib.svg'

#### 错误提示

jinja2.exceptions.TemplateNotFound: '.icons/material/pen-nib.svg' not found in search paths: ...

#### 解决方案

原因：Material主题版本与图标名称不兼容，或主题安装不完整。

方案1（最快）：删除mkdocs.yml中的自定义logo配置，注释/删除以下行：

```yaml
# logo: material/pen-nib  # 注释该行，使用默认logo
```

方案2（保留自定义logo）：重新安装稳定版本的Material主题，并替换图标名称：

```bash
pip uninstall -y mkdocs-material
pip install mkdocs-material==9.5.22  # 稳定版本
```

将mkdocs.yml中的logo配置修改为：`logo: material/pencil`（所有版本均兼容）。

### Q4：执行git commit时，提示nothing to commit, working tree clean

#### 错误提示

On branch master nothing to commit, working tree clean

#### 解决方案

原因：文件未添加到Git暂存区，或不在项目目录下，或分支名称不匹配。

1. 确认在项目目录下：`cd /c/mkdocs/mkdocs-demo-site`（对应自己的项目目录）；

2. 强制添加所有文件：`git add --all`；

3. 重新提交：`git commit -m "Initial commit: Add MkDocs config and docs structure"`；

4. 将分支重命名为main：`git branch -M main`。

### Q5：执行git push -u origin main时，提示Connection was reset

#### 错误提示

fatal: unable to access 'https://github.com/demo-user/mkdocs-demo-site.git/': Recv failure: Connection was reset

#### 解决方案

原因：HTTPS协议连接不稳定，被防火墙/代理拦截。

核心解决方案：使用SSH协议推送（参考第一部分「四、配置SSH协议」），步骤：

- 生成SSH密钥并添加到GitHub；

- 配置本地仓库的SSH远程地址；

- 重新执行`git push -u origin main`。

辅助排查：关闭代理、防火墙/杀毒软件，用手机热点测试。

### Q6：Git Bash提示demo-user@DESKTOP-XXXXXX MINGW64 ~，不知道下一步操作

#### 错误/提示说明

这不是错误，是Git Bash的正常命令提示符，说明当前处于用户主目录（`C:\Users\demo-user`，demo-user为示例用户名，XXXXXX为示例电脑名称），终端处于待命状态。

#### 解决方案

切换到MkDocs项目目录，继续执行后续命令：

```bash
cd /c/mkdocs/mkdocs-demo-site  # 切换到项目目录
```

切换后，提示符会显示项目路径，即可执行后续Git/MkDocs命令。

### Q7：执行git push时，提示The authenticity of host 'github.com (::1)' can't be established

#### 错误提示

The authenticity of host 'github.com (::1)' can't be established. ED25519 key fingerprint is: SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU Are you sure you want to continue connecting (yes/no/[fingerprint])?

#### 解决方案

原因：首次通过SSH连接GitHub，Git需要验证服务器真实性。

在提示后输入**yes**（小写）并按回车（不要输入Y或YES），后续连接不会再提示。

### Q8：执行ssh-add ~/.ssh/id_ed25519时，提示No such file or directory

#### 错误提示

/c/Users/demo-user/.ssh/id_ed25519: No such file or directory（demo-user为示例用户名）

#### 解决方案

原因：本地未生成SSH密钥，或密钥路径/文件名错误。

1. 查看.ssh文件夹：`ls ~/.ssh/`，确认无id_ed25519文件；

2. 重新生成密钥（全程按回车）：

```bash
ssh-keygen -t ed25519 -C "你的GitHub邮箱@example.com"
```

3. 验证生成：`ls ~/.ssh/`，能看到id_ed25519和id_ed25519.pub即为成功。

### Q9：执行ssh -T git@github.com时，提示Permission denied (publickey)

#### 错误提示

git@github.com: Permission denied (publickey).

#### 解决方案

原因：SSH公钥未正确添加到GitHub，或本地SSH代理未加载私钥。

方案1：重启SSH代理并加载私钥（Windows必做）：

```bash
ssh-agent -k  # 终止旧代理
eval "$(ssh-agent -s)"  # 重启代理
ssh-add ~/.ssh/id_ed25519  # 加载私钥
```

方案2：检查本地公钥与GitHub公钥一致性：

```bash
cat ~/.ssh/id_ed25519.pub  # 查看本地公钥
```

登录GitHub→SSH and GPG keys，对比公钥内容，确保完全一致（无遗漏、无多余空格）；不一致则重新添加。

方案3：使用RSA密钥（备用方案）：

```bash
ssh-keygen -t rsa -b 4096 -C "你的GitHub邮箱@example.com"  # 生成RSA密钥
clip < ~/.ssh/id_rsa.pub  # 复制公钥到GitHub
ssh-add ~/.ssh/id_rsa  # 加载私钥
```

### Q10：向GitHub添加SSH公钥时，提示Key is invalid. You must supply a key in OpenSSH public key format

#### 错误提示

Key is invalid. You must supply a key in OpenSSH public key format

#### 解决方案

原因：粘贴的公钥不符合OpenSSH格式（复制错误文件、内容不完整、有多余换行）。

1. 重新复制正确的公钥（确保是带.pub后缀的公钥文件）：

```bash
clip < ~/.ssh/id_ed25519.pub  # ED25519密钥
# 或 clip < ~/.ssh/id_rsa.pub  # RSA密钥
```

2. 粘贴到GitHub时，确保是「完整的单行字符串」，无换行、无多余空格；

3. 备用方案：强制生成OpenSSH格式密钥：

```bash
ssh-keygen -t ed25519 -C "你的GitHub邮箱@example.com" -m PEM  # 强制OpenSSH格式
```

### Q11：执行ssh -T git@github.com时，显示Hi demo-user! You've successfully authenticated, but GitHub does not provide shell access.

#### 提示说明

这不是错误，是SSH身份验证成功的提示！说明GitHub已确认你的身份（demo-user为示例用户名），可正常执行Git推送操作。

#### 下一步操作

切换到项目目录，执行推送命令：

```bash
cd /c/mkdocs/mkdocs-demo-site
git push -u origin main
```

### Q12：GitHub Actions部署失败

#### 错误/提示说明

GitHub Actions页面显示红色叉号，部署失败。

#### 解决方案

原因：Actions配置错误、Python版本不兼容、依赖安装失败。

1. 点击失败的Actions记录，查看错误提示的「Steps」；

2. 常见修正点：

- 确保Actions配置中的Python版本为3.11（与本地版本一致）；

- 重新提交Actions配置文件，确保无语法错误；

- 若依赖安装失败，本地重新执行相关`pip install`命令，验证无误后再推送。

### Q13：本地预览正常，GitHub Pages访问显示404错误

#### 错误/提示说明

浏览器访问GitHub Pages链接时，显示「404 Not Found」。

#### 解决方案

原因：GitHub Pages未正确指向构建产物目录，或Actions未构建成功。

1. 检查Actions构建状态：仓库→「Actions」，确保最新构建为绿色对勾；失败则参考Q12排查；

2. 检查GitHub Pages配置：仓库→「Settings」→「Pages」，确认「Source」为「GitHub Actions」，无其他错误配置；

3. 耐心等待：GitHub Pages生效需要5-10分钟，刷新浏览器重试；

4. 验证仓库名称：确保访问链接中的仓库名称与GitHub仓库名称完全一致（区分大小写）。

### 补充说明

所有操作均基于Windows系统（Git Bash）；Mac/Linux系统可替换路径格式（例如Windows的`/c/mkdocs`，Mac替换为`/Users/用户名/mkdocs`），命令完全一致；初学者操作时，建议逐行执行命令，不要跳过步骤；遇到本文未列出的错误，优先查看终端错误提示——多数错误会明确标注原因（如文件缺失、语法错误、网络问题），也可复制错误提示到网上搜索解决方案，多数常见MkDocs部署问题已被开发者社区讨论解决。

部署成功后，若需更新站点内容（如修改.md文档、调整mkdocs.yml配置），只需完成以下简单步骤：1. 在VS Code中编辑对应文件；2. 在Git Bash中执行`git add --all`和`git commit -m "Update website content: [修改说明]"`，提交本地修改；3. 执行`git push -u origin main`，将修改推送到GitHub。GitHub Actions会自动触发新的构建部署，更新后的内容会在5-10分钟内在公开站点生效（受GitHub缓存影响）。

需注意，全程操作中，仓库名称与项目目录名称需保持一致，避免路径混乱和部署失败；此外，建议定期备份本地项目文件，尤其是mkdocs.yml配置文件和重要的.md文档，防止因误删、系统故障导致数据丢失。初学者在无指导的情况下，不建议修改MkDocs及相关插件的默认配置，可在熟悉基础操作流程后，再逐步探索优化站点样式和功能。

最后，若想自定义站点域名（将默认的`https://你的GitHub用户名.github.io/仓库名/`替换为自己的域名），可参考GitHub官方文档的GitHub Pages域名配置教程，该步骤为可选操作，可在完全掌握基础部署流程后再实现。
> （注：文档部分内容可能由 AI 生成）