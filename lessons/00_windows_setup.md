---
layout: default
title: Windows Setup Guide
nav_order: 0
parent: Lessons
---

# Windows Setup Guide for Work Computers

**Goal:** Get Git and your development environment set up on a Windows work computer. This guide covers common scenarios including corporate restrictions and network configurations.

---

## Prerequisites

Before you begin, make sure you have:
- Administrator access to install software (or IT approval)
- A stable internet connection
- A GitHub account (create one at [github.com](https://github.com/signup) if needed)

---

## Step 1: Install Git for Windows

### Download Git
1. Go to [git-scm.com/downloads](https://git-scm.com/downloads)
2. Click **"Download for Windows"**
3. The download should start automatically

### Installation Walkthrough

Run the installer and use these recommended settings:

| Screen | Recommended Selection |
|--------|----------------------|
| **Select Components** | Keep defaults, ensure "Git Bash Here" is checked |
| **Default Editor** | Select **"Use Visual Studio Code as Git's default editor"** |
| **Initial Branch Name** | Select **"Override the default branch name"** → enter `main` |
| **PATH Environment** | Select **"Git from the command line and also from 3rd-party software"** |
| **SSH Executable** | Select **"Use bundled OpenSSH"** |
| **HTTPS Backend** | Select **"Use the native Windows Secure Channel library"** (recommended for corporate networks) |
| **Line Ending Conversions** | Select **"Checkout Windows-style, commit Unix-style line endings"** |
| **Terminal Emulator** | Select **"Use Windows' default console window"** |
| **Git Pull Behavior** | Select **"Fast-forward or merge"** |
| **Credential Manager** | Select **"Git Credential Manager"** ✅ Important! |
| **Extra Options** | Keep defaults |

{: .note }
> For corporate networks with SSL inspection, choosing "Windows Secure Channel library" helps avoid certificate issues.

---

## Step 2: Install Visual Studio Code

### Download VS Code
1. Go to [code.visualstudio.com](https://code.visualstudio.com/)
2. Click **"Download for Windows"**
3. Run the installer

### Installation Options
During installation, check these options:
- ✅ Add "Open with Code" action to Windows Explorer file context menu
- ✅ Add "Open with Code" action to Windows Explorer directory context menu
- ✅ Register Code as an editor for supported file types
- ✅ Add to PATH

### Recommended Extensions
After installing VS Code, add these extensions:
1. Open VS Code
2. Press `Ctrl+Shift+X` to open Extensions
3. Search and install:
   - **GitLens** — Enhanced Git capabilities
   - **Git Graph** — Visualize your Git history
   - **Markdown Preview Enhanced** — Better markdown editing

---

## Step 3: Verify Your Installation

Open **Git Bash** (search for it in the Start menu) and run:

```bash
# Check Git version
git --version
```

You should see output like: `git version 2.x.x.windows.x`

Open **Command Prompt** or **PowerShell** and verify:

```powershell
# Git should work from any terminal
git --version

# VS Code should be accessible
code --version
```

---

## Step 4: Configure Git

Set up your identity (this information will appear in your commits):

```bash
# Set your name (use your real name)
git config --global user.name "Your Name"

# Set your email (use the email associated with your GitHub account)
git config --global user.email "your.email@example.com"
```

### Additional Recommended Settings

```bash
# Set default branch name to 'main'
git config --global init.defaultBranch main

# Set VS Code as your default editor
git config --global core.editor "code --wait"

# Enable helpful colors in terminal output
git config --global color.ui auto

# Set up credential storage (so you don't have to enter password every time)
git config --global credential.helper manager
```

### Verify Your Configuration

```bash
git config --global --list
```

---

## Step 5: Connect to GitHub

### Option A: HTTPS (Recommended for Work Computers)

HTTPS is often easier on corporate networks. When you push/pull for the first time:
1. Git will open a browser window
2. Sign in to GitHub
3. Authorize Git Credential Manager
4. Your credentials are stored securely

### Option B: SSH Key Setup

If your organization prefers SSH:

```bash
# Generate a new SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Press Enter to accept the default file location
# Enter a passphrase (recommended) or press Enter for none
```

Add your SSH key to the ssh-agent:

```bash
# Start the ssh-agent
eval "$(ssh-agent -s)"

# Add your SSH key
ssh-add ~/.ssh/id_ed25519
```

Copy your public key to add to GitHub:

```bash
# Copy your public key to clipboard
cat ~/.ssh/id_ed25519.pub
# Select and copy the output
```

Add the key to GitHub:
1. Go to [github.com/settings/keys](https://github.com/settings/keys)
2. Click **"New SSH key"**
3. Give it a title (e.g., "Work Laptop")
4. Paste your key
5. Click **"Add SSH key"**

Test your connection:

```bash
ssh -T git@github.com
```

You should see: `Hi username! You've successfully authenticated...`

---

## Troubleshooting Common Issues

### Issue: SSL Certificate Problems

If you see SSL/TLS certificate errors on a corporate network:

```bash
# Use Windows certificate store (if Git was configured with OpenSSL)
git config --global http.sslBackend schannel
```

{: .warning }
> Never disable SSL verification (`http.sslVerify false`) as this is a security risk.

### Issue: Proxy Configuration

If your company uses a proxy:

```bash
# Set HTTP proxy
git config --global http.proxy http://proxy.company.com:8080

# Set HTTPS proxy
git config --global https.proxy http://proxy.company.com:8080
```

To check your current proxy settings:

```bash
git config --global --get http.proxy
```

### Issue: Line Ending Warnings

If you see warnings about line endings:

```bash
# This is normal on Windows - Git is converting line endings
# The setting below handles this automatically
git config --global core.autocrlf true
```

### Issue: "Permission Denied" Errors

- Make sure you're not trying to write to a protected folder
- Try running Git Bash or VS Code as Administrator
- Check if your antivirus is blocking Git operations

### Issue: Git Credential Manager Not Working

```bash
# Reinstall credential manager
git config --global credential.helper manager

# Clear stored credentials if needed
git credential-manager unconfigure
git credential-manager configure
```

---

## Quick Reference Card

| Task | Command |
|------|---------|
| Check Git version | `git --version` |
| View configuration | `git config --global --list` |
| Set username | `git config --global user.name "Name"` |
| Set email | `git config --global user.email "email"` |
| Open current folder in VS Code | `code .` |
| Open Git Bash in folder | Right-click → "Git Bash Here" |

---

## Next Steps

Once your environment is set up, proceed to [Lesson 1 — Getting Set Up](01_intro.md) to learn about Git fundamentals and your first repository!

---

{: .note }
> **Need help?** If you encounter issues specific to your company's IT policies, contact your IT department for assistance with proxy settings, certificates, or software installation permissions.
