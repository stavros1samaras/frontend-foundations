### 🎣 git fetch [options]
Downloads **objects** (commits, refs, etc.) from a **remote repository** to your local repository.

**Important:** `git fetch` **does not** merge or modify your local working files. It simply updates your **local remote-tracking branches** (e.g., `origin/main`).

| `git fetch` | Fetches all changes (commits, branches) from **all** registered remote repositories (remotes). | `git fetch` |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| `git fetch [remote]` | Fetches all changes only from the specified remote repository (e.g., `origin`). | `git fetch origin` |
| `git fetch [remote] [branch]` | Fetches only the specified branch from the specified remote repository. | `git fetch origin main` |
| `git fetch --all` | Fetches updates from all registered remote repositories. | `git fetch --all` |
| `git fetch --prune` or `-p` | Deletes any local remote-tracking branches that have been removed on the remote. | `git fetch -p origin` |

<img width="500" height="500" alt="εικόνα" src="https://github.com/user-attachments/assets/fde87260-8758-4e2c-ac9a-f1eaa5ca5785" />
---

### 🔗 git pull [options]
Downloads changes from a remote repository (`git fetch`) **and** immediately integrates them into the current local branch (`git merge`).

| `git pull` | ⭐ Downloads and merges changes from the **upstream** branch of the current branch (e.g., `origin/main`). | `git pull` |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------- | -------------------------- |
| `git pull [remote] [branch]` | Downloads and merges the specific branch from the specific remote. | `git pull origin main` |
| `git pull --rebase` | Uses `rebase` instead of `merge` to integrate changes, keeping the history cleaner. | `git pull --rebase` |




### 💡 Relationship with `git pull`
`git pull` is essentially a combination of **`git fetch`** followed by **`git merge`** (or `git rebase`, depending on configuration).

* **`git fetch`**: Downloads the changes to the **local** repository, updating references like `origin/main`, but **does not** apply them to your current local branch (e.g., `main`).
* **`git pull`**: Downloads the changes **and** automatically merges them into the current local branch.


<img width="800" height="800" alt="1_gZX2Cs-To3k1h63hHhPPcw" src="https://github.com/user-attachments/assets/2439c234-5f73-426a-b21b-1fc3749a53e8"/>



