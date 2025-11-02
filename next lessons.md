### git stash [options]
Temporarily saves (stashes) uncommitted changes so you can work on something else without committing.

| `git stash` | Saves current uncommitted changes (both staged and unstaged). | `git stash` |
| ------------ | -------------------------------- | ---- |
| `git stash push -u -m "message"` | Saves uncommitted changes including untracked files **with a custom message**. | `git stash push -u -m "Fix login bug"` |
| `git stash -u` | Saves uncommitted changes including untracked files. | `git stash -u` |
| `git stash list` | Shows all stashed changes. | `git stash list` |
| `git stash apply` | Reapplies the most recent stash without removing it from the stash list. | `git stash apply` |
| `git stash apply stash@{n}` | Reapplies a specific stash from the stash list without removing it. | `git stash apply stash@{2}` |
| `git stash pop` | Reapplies the most recent stash **and removes it** from the stash list. | `git stash pop` |
| `git stash pop stash@{n}` | Reapplies a specific stash and removes it from the stash list. | `git stash pop stash@{2}` |
| `git stash drop` | Deletes the most recent stash without applying it. | `git stash drop` |
| `git stash drop stash@{n}` | Deletes a specific stash from the stash list. | `git stash drop stash@{2}` |
| `git stash clear` | Deletes **all** stashes. | `git stash clear` |
| `git stash branch [branch-name]` | Creates a new branch from the stash and applies it there. | `git stash branch fix-bug` |
