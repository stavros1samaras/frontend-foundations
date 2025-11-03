# Re-writing history

### Fix your last commit comment

### git commit --amend [flags]
Modifies the most recent commit (e.g., to change its message or include missed files).

| `git commit --amend` | Opens the editor to modify the last commit message or include newly staged files. | `git commit --amend` |
| ---------------------- | -------------------------------- | ---- |
| `git commit --amend -m "[new message]"` | Updates the last commit with a new message (no editor). | `git commit --amend -m "Updated commit message"` |
| `git commit --amend --no-edit` | Keeps the previous commit message, only adds newly staged changes. | `git commit --amend --no-edit` |
