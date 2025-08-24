##  Why Obsidian + GitHub?

- **Obsidian** → a powerful note-taking app that stores everything as plain Markdown files (.md). All your notes are just real files on disk.

- **GitHub** → a cloud repository service based on Git. Perfect for backups, syncing, and version history.

The idea: your **Obsidian vault = a Git repository**. Every time you add/change notes, you can sync them to GitHub.

---
## Setup

1. **Install Obsidian** → [obsidian.md](https://obsidian.md/)
2. **Create a vault** (e.g. ~/Notes).
3. **Install Git** (if not installed):

```
brew install git     # macOS (via Homebrew)
sudo apt install git # Ubuntu/Debian
```

4. **Create a GitHub repo** (e.g. notes-vault) and leave it empty → don’t add README or .gitignore yet.

---
##  Connect Obsidian Vault to GitHub
In your terminal:

```
cd ~/Notes   # your Obsidian vault folder
git init
git remote add origin git@github.com:USERNAME/notes-vault.git
git branch -M main
git add .
git commit -m "Initial commit"
git push -u origin main
```

Now your entire vault is backed up on GitHub 🎉

---
## Auto-Sync Script
Instead of typing git add/commit/push manually, create a small script.
Create sync-note.sh in your home directory:

```
#!/bin/bash

# Path to Obsidian vault
VAULT_PATH="$HOME/Notes"

# Commit message with timestamp
COMMIT_MSG="Update notes $(date '+%Y-%m-%d %H:%M:%S')"

# Go to vault
cd "$VAULT_PATH" || { echo "Vault not found"; exit 1; }

# Add, commit, push
git add .
git commit -m "$COMMIT_MSG"
git push origin main

echo "✅ Vault synced!"
```

Make it executable:

```
chmod +x ~/sync-note.sh
```

Now sync with:

```
./sync-note.sh
```

---

##  Using on Another Device

On a second machine:

```
git clone ...
```

Open this folder as your vault in Obsidian. Run ./sync-note.sh whenever you want to push/pull changes.