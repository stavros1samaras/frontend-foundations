### git branch [options]
Manages branches in a Git repository (create, list, delete, or rename branches).

| `git branch` | Lists all local branches in the repository. | `git branch` |
| ------------- | -------------------------------- | ---- |
| `git branch [branch-name]` | Creates a new branch with the specified name. | `git branch feature-login` |
| `git branch -d [branch-name]` | Deletes a branch (only if it has been merged). | `git branch -d old-feature` |
| `git branch -D [branch-name]` | Force deletes a branch, even if not merged. | `git branch -D test-branch` |
| `git branch -m [new-name]` | Renames the current branch to the new name. | `git branch -m main` |
| `git branch -a` | Lists both local and remote branches. | `git branch -a` |
| `git branch -r` | Lists only remote branches. | `git branch -r` |

### git switch [options]
Used to switch between branches or create and move to a new one.  
Introduced as a simpler alternative to `git checkout` for branch operations.

| `git switch [branch-name]` | Switches to an existing branch. | `git switch main` |
| --------------------------- | -------------------------------- | ---- |
| `git switch -c [new-branch]` | Creates a new branch **and** switches to it. | `git switch -c feature-login` |
| `git switch -` | Switches back to the **previous branch**. | `git switch -` |
| `git switch --detach [commit]` | Checks out a specific commit in a detached HEAD state (not a branch). | `git switch --detach a1b2c3d` |

---

### git checkout [options]
Used to switch branches, restore files, or view previous commits.  
Before `git switch` existed, `git checkout` handled both branch and file operations.

| `git checkout [branch-name]` | Switches to an existing branch. | `git checkout develop` |
| ----------------------------- | -------------------------------- | ---- |
| `git checkout -b [new-branch]` | Creates a new branch **and** switches to it. | `git checkout -b feature-auth` |
| `git checkout [commit-hash]` | Moves to a specific commit (detached HEAD state). | `git checkout a1b2c3d` |
| `git checkout -- [filename]` | Restores a file to its last committed state. | `git checkout -- index.html` |
| `git checkout .` | Restores **all** modified files to their last committed versions. | `git checkout .` |