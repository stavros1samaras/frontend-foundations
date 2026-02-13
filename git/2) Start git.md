#### To create an empty Git repository
- Navigate to your desired directory then type:
```bash 
git init
```

#### To download an existing Git repository
- Navigate to your desired directory then type:
```bash 
git clone "...."
```

### git clone [options]
Creates a local copy of a remote repository (downloads all files, branches, and history).

| `git clone [url]` | Clones a remote repository into a new local directory. | `git clone https://github.com/user/project.git` |
| ------------------ | -------------------------------- | ---- |
| `git clone [url] [folder-name]` | Clones the repository into a specific folder name. | `git clone https://github.com/user/project.git my-project` |
| `git clone -b [branch-name] [url]` | Clones a specific branch instead of the default one. | `git clone -b develop https://github.com/user/project.git` |
| `git clone --single-branch [url]` | Clones only the latest snapshot of a single branch (no full history). | `git clone --single-branch https://github.com/user/project.git` |
| `git clone --depth [n] [url]` | Creates a **shallow clone** with the last *n* commits (faster, smaller). | `git clone --depth 1 https://github.com/user/project.git` |
| `git clone --recurse-submodules [url]` | Clones the main repo **and all its submodules** recursively. | `git clone --recurse-submodules https://github.com/user/project.git` |

when you clone a repository git create a connection (origin) between the main remote branch (main or master) and your local branch.   your local branch will be named as the main remote branch (main or master).

if you want to go to the other remote branches but localy checkout origin/<branch> is not the correct command because this will put your in detached HEAD.
so if you want your own local branch called <remote-branch-name> and you want to be connened to origin/<remote-branch-name> just like your local master branch is connected to origin/master the correct way is to use:
```bash
 git switch <remote-branch-name>
```
to create a new local branch from the remote branch of the same name.
git switch <remote-branch-name> makes me a local <remote-branch-name> branch AND sets it up to track the remote branch origin/<remote-branch-name>.

### Example
git clone https://github.com/user/project.git
After cloning, you have:
- remote: origin
- remote branch: origin/main
- local branch: main (tracking origin/main)

Suppose the remote repository also has:
`origin/dev`

❌ Wrong way (detached HEAD)
`git checkout origin/dev`

✅ Correct way
`git switch dev`
This creates a local branch 'dev' that tracks 'origin/dev'
and switches you to it, just like 'main' tracks 'origin/main'
