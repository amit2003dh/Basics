
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

If you want, I can convert this into a **1-page revision sheet** or **interview-focused Git crash sheet**.
