### git log [options]
Shows the commit logs.

| `git log` | Shows commit history (SHA, author, date, message). | `git log` |
| ----------- | -------------------------------- | ---- |
| `git log --oneline` | Compact: one-line per commit (short SHA + message). | `git log --oneline` |
| `git log --graph` | ASCII graph of branches & merges (visualizes history). | `git log --graph` |

### git status [options]

| `git status` | Shows the current state of the working directory and staging area. | `git status` |
| ------------- | -------------------------------- | ---- |
| `git status -s` | Short (summary) format showing changes as two-letter codes (e.g., `M`, `A`, `??`). | `git status -s` |
| `git status -b` | Shows the current branch and tracking info along with the status. | `git status -b` |

### git diff [options]
Shows the differences between commits, branches, or the working directory and the staging area.

| `git diff` | Shows unstaged changes (differences between working directory and staging area). | `git diff` |
| ----------- | -------------------------------- | ---- |
| `git diff --staged` | Shows differences between the staging area and the last commit (staged changes). | `git diff --staged` |
| `git diff [branch1] [branch2]` | Compares differences between two branches. | `git diff main develop` |
| `git diff [commit1] [commit2]` | Shows changes between two commits. | `git diff a1b2c3d e4f5g6h` |
| `git diff --name-only` | Lists only filenames that have changed. | `git diff --name-only` |
| `git diff --stat` | Displays a summary of changed files and line counts. | `git diff --stat` |

---
