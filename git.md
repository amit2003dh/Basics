
Here’s your **clean, structured, interview-ready Git notes** — simplified and upgraded.

---

# 🚀 Git & GitHub – Clean Notes

## 1️⃣ Git vs GitHub

* **Git** → Version control tool (tracks code changes locally)
* **GitHub** → Cloud platform to host Git repositories

---

# 📦 Repository Setup

```bash
git init              # Initialize repository
git status            # Check file status
git add <file>        # Stage file
git add .             # Stage all files
git commit -m "msg"   # Commit changes
ls -al                # List files (detailed view)
```

---

# ⚙️ Git Configuration

```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

---

# 🔍 Viewing Changes & History

```bash
git log                # Full commit history
git log --oneline      # Compact history
git log --graph        # Visual branch graph
```

### Compare Changes

```bash
git diff               # Unstaged changes (line by line)
git diff --stat        # Summary of changes
git diff --staged      # Staged changes
```

---

# ✏️ Modify Last Commit

```bash
git commit --amend     # Edit last commit
```

---

# 🌿 Branching

```bash
git branch                    # List branches
git branch new-branch         # Create branch
git checkout new-branch       # Switch branch (old way)
git switch new-branch         # Switch branch (modern way)
git merge branch-name         # Merge into current branch
```

---

# 🌍 Remote & Collaboration

```bash
git clone <repo-url>                # Clone repository
git remote add upstream <url>       # Add original repo
git fetch upstream                  # Get updates
```

---

# 🔄 Contribution Workflow (Open Source)

1. Fork repository
2. Clone your fork
3. Create branch
4. Make changes
5. Commit
6. Push
7. Create Pull Request

---

# 📁 .gitignore

```bash
touch .gitignore
```

* Used to ignore files from tracking
* Example: `node_modules/`, `.env`, `dist/`

---

# 🖥 Install Git

### Ubuntu

```bash
sudo apt install git
```

### macOS

```bash
brew install git
```

---

# 📝 Vim Shortcuts (During Commit)

* `:q!` → Quit without saving
* `:wq` → Save & quit
* `:q` → Quit

---

Here’s your **1-Page Git Crash Sheet (Interview + Practical Use)** — minimal, sharp, high-signal.

---


# 🚀 GIT – 1 Page Power Revision

## 🔹 Core Concept (Interview Line)

> Git is a distributed version control system that tracks file changes using snapshots and enables branching, merging, and collaboration.

---

# 🧠 Git Architecture (Must Know)

**Working Directory → Staging Area → Local Repository → Remote Repository**

```bash
git add        # Working → Staging
git commit     # Staging → Local repo
git push       # Local → Remote
```

---

# ⚡ Daily Workflow

```bash
git clone <url>
git switch -c feature-x
# make changes
git add .
git commit -m "feature added"
git push origin feature-x
```

---

# 🔍 Debug & Inspect Like a Pro

```bash
git status
git diff
git diff --staged
git log --oneline --graph --all
```

---

# 🌿 Branch Mastery

```bash
git branch
git switch branch-name
git switch -c new-branch
git merge branch-name
```

Interview Tip:

* Branch = lightweight pointer
* Merge = combines histories
* No new copy created, just pointer movement + merge commit (if needed)

---

# 🧨 Fix Mistakes (Very Important)

### Unstage file

```bash
git restore --staged file
```

### Discard local changes

```bash
git restore file
```

### Undo last commit (keep changes)

```bash
git reset --soft HEAD~1
```

### Undo last commit (remove changes)

```bash
git reset --hard HEAD~1
```

---

# 🌍 Collaboration Model

```bash
git remote -v
git fetch
git pull
git push
```

**Open Source Flow**
Fork → Clone → Branch → Commit → Push → Pull Request

---

# 📁 .gitignore

Used to prevent tracking:

```
node_modules/
.env
dist/
```

---

# 🏆 Interview Power Questions

**Q: Difference between git fetch and git pull?**

* fetch → download changes
* pull → fetch + merge

**Q: What is HEAD?**

* Pointer to current commit

**Q: What is rebase?**

* Rewrites history to create linear commits

**Q: Fast-forward merge?**

* No divergence → branch pointer moves forward

---

# 💡 Advanced Edge

```bash
git stash
git rebase branch-name
git cherry-pick <commit-id>
git log --since="2 days ago"
```

---


