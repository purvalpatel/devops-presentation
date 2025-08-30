install & first-time setup
--------------------------
```
# Linux (Debian/Ubuntu)
sudo apt update && sudo apt install -y git

# macOS (with Homebrew)
brew install git

# Windows
# Install Git for Windows from git-scm.com and use "Git Bash"

# identify yourself (one-time, per machine)
git config --global user.name  "Your Name"
git config --global user.email "you@example.com"

# quality-of-life
git config --global init.defaultBranch main
git config --global pull.rebase false     # or true if you prefer rebase-on-pull
git config --global color.ui auto

```
### start or get a repo

```
# start a new repo in the current folder
git init

# clone an existing repo
git clone https://github.com/owner/project.git
# or with SSH (recommended once keys are set up)
git clone git@github.com:owner/project.git

```
