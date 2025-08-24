notes-itmo-is is my personal notes space.
# Auto-syncing script
```bash
#!/bin/bash

# Way to Obsidian vault
VAULT_PATH="$HOME/..."

# Commit message with date and time
COMMIT_MSG="Update notes $(date '+%Y-%m-%d %H:%M:%S')"

# going to vault
cd "$VAULT_PATH" || { echo "Vault was not found"; exit 1; }

# adding changes
git add .

# making a commit
git commit -m "$COMMIT_MSG"

# pushing to GitHub
git push origin main

echo "Vault is ready! ✅"
```

Don't forget to run before first usage:
```bash
chmod +x sync-note.sh
```

Sync command:
```bash
./sync-note.sh
```
