### Checking Out Old Commits
Moves your working directory to a specific commit in the repository’s history.
It allows you to explore or test the project as it existed at that point in time.
When doing so, Git enters a detached HEAD state, meaning you are not on any branch.
You can view or modify files, but any new commits won’t belong to a branch unless you create one.

Purpose:
To inspect, test, or create a new branch from a previous state of the project.
```bash
               HEAD (refers to branch 'master')
                |
                v
a---b---c---d  branch 'master' (refers to commit 'd')
```
`git checkout <commit>`
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
