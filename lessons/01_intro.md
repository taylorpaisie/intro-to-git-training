---
layout: default
title: Lesson 1 — Getting Set Up
nav_order: 1
parent: Lessons
---

# Lesson 1 — Getting Set Up

**Goal:** Set up your Git environment, configure your development tools, and establish a connection with GitHub. This lesson will ensure you have everything you need to start version controlling your projects.

## What is Git?

Git is a distributed version control system that helps you track changes in your code, collaborate with others, and maintain a history of your project. It was created by Linus Torvalds in 2005 for developing the Linux kernel and has since become the standard for version control.

---

## 1. Installing Required Tools

### Essential Tools
- **Git:** [Download from git-scm.com](https://git-scm.com/downloads)
- **VS Code (recommended):** [Download from code.visualstudio.com](https://code.visualstudio.com/)

### Installation Tips
- **Windows Users:**
  - Accept "Git Credential Manager" during installation
  - Choose "Use Visual Studio Code as Git's default editor" if prompted
  - Select "Git from the command line and also from 3rd-party software"
  - For line endings, choose "Checkout Windows-style, commit Unix-style"

- **macOS Users:**
  - On first `git` use, macOS may prompt to install developer tools—allow it
  - Install Homebrew (optional but recommended): `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
  - If using Homebrew: `brew install git`

- **Linux Users:**
  - Ubuntu/Debian: `sudo apt-get update && sudo apt-get install git`
  - Fedora: `sudo dnf install git`

## 2. Verifying Your Installation

Check that everything is installed correctly:

```bash
# Check Git version
git --version

# Check VS Code version (if installed)
code --version

# Verify Git is in your PATH
where git  # Windows
which git  # macOS/Linux
```

## 3. First-Time Git Configuration

Configure your identity (required for commits):

```bash
# Set your name
git config --global user.name "Your Name"

# Set your email (use your GitHub email)
git config --global user.email "your.email@example.com"

# Set your default branch name
git config --global init.defaultBranch main

# Set your default editor (if using VS Code)
git config --global core.editor "code --wait"
```

### Optional but Recommended Configuration

```bash
# Enable colorful Git output
git config --global color.ui auto

# Set up git to use VS Code for diffs
git config --global diff.tool vscode
git config --global difftool.vscode.cmd "code --wait --diff $LOCAL $REMOTE"

# Configure line ending behavior
git config --global core.autocrlf true  # Windows
git config --global core.autocrlf input # macOS/Linux
```

## 4. Setting up GitHub Authentication

### Using SSH (Recommended)

1. Check for existing SSH keys:
```bash
ls -la ~/.ssh
```

2. Generate a new SSH key if needed:
```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

3. Start the SSH agent:
```bash
# Windows (PowerShell)
Get-Service ssh-agent | Set-Service -StartupType Automatic
Start-Service ssh-agent

# macOS/Linux
eval "$(ssh-agent -s)"
```

4. Add your SSH key to the agent:
```bash
ssh-add ~/.ssh/id_ed25519
```

5. Copy your public key:
```bash
# Windows (PowerShell)
Get-Content ~/.ssh/id_ed25519.pub | Set-Clipboard

# macOS
pbcopy < ~/.ssh/id_ed25519.pub

# Linux
xclip -sel clip < ~/.ssh/id_ed25519.pub
```

6. Add the key to your GitHub account:
   - Go to GitHub → Settings → SSH and GPG keys
   - Click "New SSH key"
   - Paste your key and save

### Using Git Credential Manager (Alternative)

If you accepted Git Credential Manager during installation, it should work automatically when you first interact with GitHub.

## 5. Verifying GitHub Connection

Test your SSH connection:
```bash
ssh -T git@github.com
```

You should see a message like: "Hi username! You've successfully authenticated..."

## 6. Installing Useful VS Code Extensions

Open VS Code and install these recommended extensions:
- GitLens
- Git History
- Git Graph

To install from the command line:
```bash
code --install-extension eamodio.gitlens
code --install-extension donjayamanne.githistory
code --install-extension mhutchie.git-graph
```

## 7. Verify Everything Works

1. Create a test repository:
```bash
mkdir git-test
cd git-test
git init
```

2. Create and commit a test file:
```bash
echo "# Test Repository" > README.md
git add README.md
git commit -m "Initial commit"
```

If these commands work without errors, you're ready to start using Git!
