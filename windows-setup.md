---
layout: post
title: Windows Setup Guide
description: Get Git and development tools ready on Windows
image: /images/phd101212s.png
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
| 👤 **GitLab Account** | Use your company GitLab account on **https://gitlab.technomics.net** |
| 📧 **Work Email** | You'll use this for Git commits and GitLab |

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

| Extension | Purpose |
|-----------|---------|
| **GitLens** | See who changed each line, compare branches, view history |
| **Git Graph** | Visualize branches and commits in a graph |
| **GitLab Workflow** | Create/view merge requests and issues from VS Code |

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
