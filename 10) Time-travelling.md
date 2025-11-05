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
| `git checkout HEAD` | Restores all files in the working directory to the state of the last commit (discarding uncommitted changes). | `git checkout HEAD` |
| `git checkout HEAD <file>` | Restores **only the specified file** to its state in the last commit, discarding uncommitted changes to that file. | `git checkout HEAD index.html` |

instead of using git checkout HEAD <file> you can doy the same work with `git restore <file>

| Command | Description | Example |
| `git restore <file>` | Restores the specified file to its state in the last commit, discarding uncommitted changes. | `git restore index.html` |
|---------|-------------|---------|
| `git restore .` | Restores all files in the working directory to their state in the last commit, discarding all uncommitted changes. | `git restore .` |

