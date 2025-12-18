---
layout: default
title: Windows Setup Guide
nav_order: 0
parent: Lessons
---

# 🖥️ Windows Setup Guide for Work Computers

{: .highlight }
> **⏱️ Estimated Time:** 15-20 minutes

**Goal:** Get Git and your development environment set up on a Windows work computer. This guide covers common scenarios including corporate restrictions and network configurations.

---

## 📋 Prerequisites

{: .important }
> Before you begin, ensure you have the following ready:

| Requirement | Details |
|-------------|---------|
| 💻 **Admin Access** | Administrator rights to install software, or IT pre-approval |
| 🌐 **Internet Connection** | Stable connection to download installers (~100 MB total) |
| 👤 **GitLab Account** | Use your company GitLab account, or create one on [gitlab.com](https://gitlab.com/users/sign_up) |
| 📧 **Work Email** | You’ll use this for Git commits and GitLab |

---

## Step 1: Install Git for Windows

### 📥 Download Git

1. Navigate to **[git-scm.com/downloads/win](https://git-scm.com/downloads/win)**
2. Click the **"Click here to download"** link for the latest version
3. Save the installer to your Downloads folder

{: .note }
> **Current Version:** Git 2.47+ is recommended. The installer is approximately 60 MB.

### 🔧 Installation Walkthrough

Run the installer (`Git-2.x.x-64-bit.exe`) and follow these recommended settings:

<details>
<summary><strong>📋 Click to expand full installation options</strong></summary>

| Step | Screen | Recommended Selection |
|------|--------|----------------------|
| 1 | **Select Components** | ✅ Keep defaults<br>✅ Ensure "Git Bash Here" is checked<br>✅ Ensure "Git GUI Here" is checked |
| 2 | **Default Editor** | Select **"Use Visual Studio Code as Git's default editor"** |
| 3 | **Initial Branch Name** | Select **"Override the default branch name"** → type `main` |
| 4 | **PATH Environment** | Select **"Git from the command line and also from 3rd-party software"** |
| 5 | **SSH Executable** | Select **"Use bundled OpenSSH"** |
| 6 | **HTTPS Backend** | ⭐ Select **"Use the native Windows Secure Channel library"** |
| 7 | **Line Ending Conversions** | Select **"Checkout Windows-style, commit Unix-style line endings"** |
| 8 | **Terminal Emulator** | Select **"Use Windows' default console window"** |
| 9 | **Git Pull Behavior** | Select **"Fast-forward or merge"** (default) |
| 10 | **Credential Manager** | ⭐ Select **"Git Credential Manager"** — This is important! |
| 11 | **Extra Options** | ✅ Enable file system caching<br>✅ Enable symbolic links (if available) |

</details>

{: .warning }
> **Corporate Networks:** Step 6 (HTTPS Backend) is critical! Selecting "Windows Secure Channel library" uses your company's certificate store and avoids SSL errors.

---

## Step 2: Install Visual Studio Code

VS Code is a free, powerful code editor with excellent Git integration.

### 📥 Download VS Code

1. Navigate to **[code.visualstudio.com](https://code.visualstudio.com/)**
2. Click the blue **"Download for Windows"** button
3. Run the installer (`VSCodeUserSetup-x64-1.x.x.exe`)

### 🔧 Installation Options

During installation, **check all of these boxes**:

```
✅ Create a desktop icon
✅ Add "Open with Code" action to Windows Explorer file context menu
✅ Add "Open with Code" action to Windows Explorer directory context menu  
✅ Register Code as an editor for supported file types
✅ Add to PATH (requires shell restart)
```

{: .note }
> The "Add to PATH" option lets you open VS Code from any terminal by typing `code`.

### 🧩 Recommended Extensions

After installing VS Code, enhance it with these Git-focused extensions:

1. Open VS Code
2. Press `Ctrl+Shift+X` to open the Extensions panel
3. Search for and install each extension:

| Extension | Purpose | Install Link |
|-----------|---------|--------------|
| **GitLens** | See who changed each line, compare branches, view history | [Install](vscode:extension/eamodio.gitlens) |
| **Git Graph** | Visualize branches and commits in a graph | [Install](vscode:extension/mhutchie.git-graph) |
| **GitLab Workflow** | Create/view merge requests and issues from VS Code | [Install](vscode:extension/gitlab.gitlab-workflow) |

<details>
<summary><strong>🎨 Optional: Additional helpful extensions</strong></summary>

| Extension | Purpose |
|-----------|---------|
| **Markdown Preview Enhanced** | Better markdown editing and preview |
| **Code Spell Checker** | Catch typos in your code and comments |
| **Material Icon Theme** | Better file icons in the explorer |

</details>

---

## Step 3: Verify Your Installation

Let's make sure everything is working correctly.

### ✅ Test Git

Open **Git Bash** (search for "Git Bash" in the Start menu):

```bash
git --version
```

{: .highlight }
> **Expected output:** `git version 2.47.0.windows.1` (or similar)

### ✅ Test VS Code

In the same Git Bash window:

```bash
code --version
```

{: .highlight }
> **Expected output:** Version number like `1.95.0` followed by a commit hash

### ✅ Test Both Together

```bash
# This should open VS Code in the current directory
code .
```

If VS Code opens, you're all set! 🎉

{: .warning }
> **Not working?** If `code` command isn't found, restart your terminal or computer. The PATH update requires a fresh terminal session.

---

## Step 4: Configure Git

Now let's set up your Git identity. This information appears in every commit you make.

### 👤 Set Your Identity

Open **Git Bash** and run these commands (replace with your actual info):

```bash
# Set your name (this will appear in your commits)
git config --global user.name "Taylor Paisie"

# Set your email (use the same email you use in GitLab)
git config --global user.email "taylor.paisie@example.com"
```

{: .important }
> Use your **real name** and the **email associated with your GitLab account**. This is how your commits are attributed to you.

### ⚙️ Recommended Settings

Copy and paste this entire block to configure best practices:

```bash
# Set default branch name to 'main' (modern standard)
git config --global init.defaultBranch main

# Set VS Code as your default Git editor
git config --global core.editor "code --wait"

# Enable colorful terminal output
git config --global color.ui auto

# Store credentials securely with Git Credential Manager
git config --global credential.helper manager

# Handle line endings properly on Windows
git config --global core.autocrlf true

# Set a helpful pull behavior
git config --global pull.rebase false
```

### 🔍 Verify Your Configuration

Check that everything is set correctly:

```bash
git config --global --list
```

You should see output similar to:

```
user.name=Taylor Paisie
user.email=taylor.paisie@example.com
init.defaultbranch=main
core.editor=code --wait
color.ui=auto
credential.helper=manager
core.autocrlf=true
pull.rebase=false
```

---

## Step 5: Connect to GitLab

You need to authenticate with GitLab to push and pull code. Choose the method that works best for your environment.

### 🔐 Option A: HTTPS with Credential Manager (Recommended)

{: .highlight }
> **Best for:** Most work computers, especially those on corporate networks

This is the easiest method and works well with corporate proxies and firewalls.

**How it works:**
1. The first time you `git push` or `git pull`, a browser window may open
2. Sign in to your GitLab account
3. Click **"Authorize"** to grant access
4. Git Credential Manager stores your credentials securely
5. Future operations work automatically!

**Test it:**
```bash
# Clone a repository you have access to (this will trigger authentication)
# Example (GitLab.com):
# git clone https://gitlab.com/<group-or-user>/<project>.git

# Example (self-managed GitLab):
# git clone https://gitlab.example.com/<group>/<project>.git
```

---

### 🔑 Option B: SSH Keys (Advanced)

{: .note }
> **Best for:** Users comfortable with terminal commands, or when HTTPS doesn't work

<details>
<summary><strong>📋 Click to expand SSH setup instructions</strong></summary>

#### Generate an SSH Key

```bash
# Generate a new SSH key pair
ssh-keygen -t ed25519 -C "your.email@example.com"
```

When prompted:
- **File location:** Press `Enter` to accept default (`~/.ssh/id_ed25519`)
- **Passphrase:** Enter a secure passphrase (recommended) or press `Enter` for none

#### Start the SSH Agent

```bash
# Start the ssh-agent in the background
eval "$(ssh-agent -s)"

# Add your private key to the agent
ssh-add ~/.ssh/id_ed25519
```

#### Copy Your Public Key

```bash
# Display your public key
cat ~/.ssh/id_ed25519.pub
```

Select and copy the entire output (starts with `ssh-ed25519`).

#### Add Key to GitLab

1. Go to your GitLab profile SSH keys page:
   - GitLab.com: https://gitlab.com/-/profile/keys
   - Self-managed: User Settings → **SSH Keys**
2. Click **"New SSH key"**
3. **Title:** Enter a descriptive name (e.g., "Work Laptop - December 2024")
4. **Key type:** Keep as "Authentication Key"
5. **Key:** Paste your public key
6. Click **"Add SSH key"**

#### Test Your Connection

```bash
# GitLab.com
ssh -T git@gitlab.com

# Self-managed GitLab (example)
# ssh -T git@gitlab.example.com
```

{: .highlight }
> **Expected output:** You should see a welcome/authentication message from GitLab.

</details>

---

## 🔧 Troubleshooting Common Issues

<details>
<summary><strong>❌ SSL Certificate Errors</strong></summary>

**Symptom:** `SSL certificate problem: unable to get local issuer certificate`

**Cause:** Corporate networks often use SSL inspection, which can interfere with Git's certificate verification.

**Solution:**
```bash
# Switch to Windows certificate store
git config --global http.sslBackend schannel
```

{: .warning }
> **Never** run `git config --global http.sslVerify false` — this disables security and exposes you to man-in-the-middle attacks.

</details>

<details>
<summary><strong>🌐 Proxy Configuration</strong></summary>

**Symptom:** Git operations hang or timeout

**Cause:** Your company network requires a proxy for internet access.

**Solution:**
```bash
# Set proxy (ask IT for the correct proxy address)
git config --global http.proxy http://proxy.yourcompany.com:8080
git config --global https.proxy http://proxy.yourcompany.com:8080

# To check current proxy settings
git config --global --get http.proxy

# To remove proxy settings (if working from home)
git config --global --unset http.proxy
git config --global --unset https.proxy
```

{: .note }
> Some companies use different proxies for different networks. You may need to update these settings when switching between office and home.

</details>

<details>
<summary><strong>⚠️ Line Ending Warnings</strong></summary>

**Symptom:** `warning: LF will be replaced by CRLF`

**Cause:** Windows and Unix use different line endings. Git is automatically converting them.

**Solution:** This warning is normal and expected on Windows. The conversion helps maintain compatibility:

```bash
# Ensure autocrlf is enabled (should already be set)
git config --global core.autocrlf true
```

</details>

<details>
<summary><strong>🚫 Permission Denied Errors</strong></summary>

**Symptom:** `error: unable to create file ... Permission denied`

**Possible causes and solutions:**

| Cause | Solution |
|-------|----------|
| Protected folder | Don't use `C:\Program Files` or system folders for repositories |
| File in use | Close any programs that might have the file open |
| Antivirus blocking | Add Git to your antivirus exceptions |
| Need admin rights | Right-click Git Bash → "Run as administrator" |

</details>

<details>
<summary><strong>🔑 Credential Manager Issues</strong></summary>

**Symptom:** Git keeps asking for your password, or authentication fails

**Solutions:**

```bash
# Verify credential helper is configured
git config --global credential.helper

# Should output: manager

# If credentials are corrupted, clear them
# Open Windows Credential Manager:
# Control Panel → User Accounts → Credential Manager → Windows Credentials
# Find and remove entries starting with "git:" or entries related to your GitLab host

# Then reconfigure
git config --global credential.helper manager
```

</details>

<details>
<summary><strong>💻 'code' Command Not Found</strong></summary>

**Symptom:** `bash: code: command not found`

**Solutions:**

1. **Restart your terminal** — PATH changes require a new session
2. **Reinstall VS Code** with "Add to PATH" checked
3. **Manual fix** — Add VS Code to PATH:
   - Search "Environment Variables" in Windows
   - Edit "Path" under User variables
   - Add: `C:\Users\YOUR_USERNAME\AppData\Local\Programs\Microsoft VS Code\bin`

</details>

---

## 📋 Quick Reference Card

### Essential Commands

| Task | Command |
|------|---------|
| Check Git version | `git --version` |
| Open VS Code in current folder | `code .` |
| Open Git Bash in any folder | Right-click → **"Git Bash Here"** |
| View all Git settings | `git config --global --list` |
| Edit Git settings file | `git config --global --edit` |

### Configuration Commands

| Task | Command |
|------|---------|
| Set your name | `git config --global user.name "Your Name"` |
| Set your email | `git config --global user.email "email@example.com"` |
| Set default editor | `git config --global core.editor "code --wait"` |
| Set default branch | `git config --global init.defaultBranch main` |

### Keyboard Shortcuts (VS Code)

| Action | Shortcut |
|--------|----------|
| Open Command Palette | `Ctrl+Shift+P` |
| Open Source Control | `Ctrl+Shift+G` |
| Open Terminal | `` Ctrl+` `` |
| Open Extensions | `Ctrl+Shift+X` |
| Open Settings | `Ctrl+,` |

---

## ✅ Setup Checklist

Before moving on, verify you've completed each step:

- [ ] Git installed and `git --version` works
- [ ] VS Code installed and `code .` opens it
- [ ] GitLens extension installed
- [ ] Git configured with your name and email
- [ ] Successfully authenticated with GitLab (HTTPS or SSH)
- [ ] Cloned a test repository successfully

---

## 🎯 Next Steps

Congratulations! Your Windows environment is ready for Git. 🎉

{: .highlight }
> **Continue to:** [Lesson 1 — Getting Set Up](01_intro.md) to learn Git fundamentals and create your first repository!

---

## 📚 Additional Resources

| Resource | Link |
|----------|------|
| Git Documentation | [git-scm.com/doc](https://git-scm.com/doc) |
| GitLab Docs | [docs.gitlab.com](https://docs.gitlab.com) |
| VS Code Git Guide | [code.visualstudio.com/docs/sourcecontrol/overview](https://code.visualstudio.com/docs/sourcecontrol/overview) |
| Interactive Git Tutorial | [learngitbranching.js.org](https://learngitbranching.js.org/) |

---

{: .note }
> **Need help?** If you encounter issues specific to your company's IT policies, contact your IT department for assistance with proxy settings, certificates, or software installation permissions.
