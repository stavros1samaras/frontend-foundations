## Checking Out Old Commits
Moves your working directory to a specific commit in the repository’s history.
It allows you to explore or test the project as it existed at that point in time.
When doing so, Git enters a detached HEAD state, meaning you are not on any branch.
You can view or modify files, but any new commits won’t belong to a branch unless you create one.

Purpose:
To inspect, test, or create a new branch from a previous state of the project.

`git checkout <commitId>` or `git checkout HEAD~<number>`
```bash
               HEAD (refers to branch 'master')
                |
                v
a---b---c---d  branch 'master' (refers to commit 'd')
```
Example: `git checkout b` or `git checkout HEAD~3`
```bash
   HEAD (refers to commit 'b')
    |
    v
a---b---c---d  branch 'master' (refers to commit 'd')
```
To go to previous situation type 
`git checkout -
`
OR
`git switch master`

## Discarding Changes

| Command | Description | Example |
|----------|--------------|----------|
| `git checkout HEAD` | ⭐ Restores all files in the working directory to the state of the last commit (discarding uncommitted changes). | `git checkout HEAD` |
| `git checkout HEAD <file>` | Restores **only the specified file** to its state in the last commit, discarding uncommitted changes to that file. | `git checkout HEAD index.html` |

instead of using git checkout HEAD <file> you can doy the same work with `git restore <file>`
that restores working directory files to a previous state — used to discard local changes or unstage files without affecting commits.

| `git restore <file>` | Restores the specified file to its state in the last commit, discarding uncommitted changes. | `git restore index.html` |
|---------|-------------|---------|
| `git restore .` | ⭐ Restores all files in the working directory to their state in the last commit, discarding all uncommitted changes. | `git restore .` |
| `git restore --staged <file>` | Unstages the specified file (removes it from the staging area) without changing the working directory. | `git restore --staged index.html` |


git reset: Moves the current branch (HEAD) to a specific commit — used to undo commits or unstage changes, optionally altering the working directory.

| `git reset --soft <commit>` | ⭐ Moves HEAD to the specified commit but keeps both staged and working directory changes (useful to redo a commit). | `git reset --soft HEAD~1` |
|----------|-------------|----------|
| `git reset <file>` | Unstages the specified file, keeping the changes in the working directory. | `git reset index.html` |
| `git reset` | ⭐ Unstages all files that are currently staged for commit, keeping their changes in the working directory. | `git reset` |
| `git reset --mixed <commit>` | Moves HEAD to the specified commit and unstages all changes, but keeps them in the working directory (default mode). | `git reset --mixed HEAD~1` |
| `git reset --hard <commit>` | Moves HEAD to the specified commit and **discards all changes** in both the staging area and working directory. | `git reset --hard HEAD~1` |
| `git reset --hard` | Resets the current branch to the last commit, discarding all uncommitted changes. | `git reset --hard` |

