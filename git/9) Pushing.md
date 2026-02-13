### git push [options]
Uploads local commits to a remote repository (sends your changes to GitHub, GitLab, etc.).

| `git push [remote] [branch]` | Pushes the specified branch to the remote repository. | `git push origin main` |
| ----------------------------- | -------------------------------- | ---- |
| `git push -u [remote] [branch]` | Pushes and sets the branch to track the remote one (used the first time). | `git push -u origin main` |
| `git push --force` | Forces an update on the remote branch (overwrites history — **use with caution!**). | `git push --force origin main` |
| `git push --all` | Pushes all local branches to the remote. | `git push --all origin` |
| `git push --tags` | Pushes all tags to the remote repository. | `git push --tags` |
| `git push [remote] :[branch]` | Deletes a branch from the remote repository. | `git push origin :old-feature` |