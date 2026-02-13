
# Git Commands Cheat Sheet and Practices

A brief description of what this project does and who it's for


## 1. Git Configuration

### Set your user name and email (only once per computer)

To deploy this project run

```bash
git config --global user.name "Your Name"
git config --global user.email "email@domain.com"
```

## 2. If You Already Have a Project in VSCode
### Initialize Git locally, commit your files, and push to GitHub

```bash
git init
git add .      ({review each change})
git add -p
git commit -m "YOUR MESSAGE"
git remote add origin https://github.com/stavros1samaras/[yourRepository].git
git branch -M main
git push -u origin main
```

## 3. Link an Existing GitHub Repo with Your Local Repo
### If the repo already exists on GitHub

```bash
git init
git remote add origin <URL_of_your_Repo>
git add .
git commit -m "Local changes"
git branch -M main
git push -u origin main
```

## 4. Clone an Existing Repo from GitHub
### Copy a repo to a new local folder

```bash
git clone <URL_of_your_Repo>
cd <folder_name>
git add .
git commit -m "My changes"
git push -u origin main
````

# Βranches


#### ονομαζω το κυριο branch se main σε περιπτωση που λεγεται master
```bash
git branch -M main
```

#### συνδεω γκιτ με γκιτχαμπ αλλιως δεν εχω μπραντσις
```bash
git remote add origin https://github.com/stavros1samaras/gitExample.git
git add .
git commit -m "first commit"
```

#### κανω push -u γιατι ειναι η πρωτη φορα που κανω push
```bash
git push -u origin main
```

#### αλλαζω branch και το δημιουργω ταυτοχρoνα
```bash
git switch -c temp
git add readMe2.txt
git commit -m "readMe2 added"
```

#### ξανα κανω push -u γιατι ειναι η πρωτη φορα που κανω push στο temp branch
```bash
git push -u origin temp
```

#### εδω βλεπω τα 2 branches μου main και temp
```bash
git branch
git switch main
```

#### αυτο ειναι το ιστορικο του branch
```bash
git log --oneline
```
#### ειμαι στο main και θελω να το κανω merge με το temp
```bash
git merge temp
```
#### το git ενημερωθηκε αλλα πρεπει να ενημερωθει και το github
```bash
git push origin main / git push (αμα ειμαι ακομα στο main)
```
### διαγραφη temp

#### βλεπω τα branches του github
```bash
git branch -r
```
#### βλεπω τα branches του git
```bash
git branch -l
```
#### διαγραφω local το temp
```bash
git branch -d temp
```
#### στο remote εχω 2 branches ενω στο local εχω 1 branch
```bash
git branch -r
git branch -l
```
#### διαγραφω και το remode branch
```bash
git push origin --delete temp
```
#### ξαναβλεπω τα branches μου και ολα καλα
```bash
git branch -r
git branch -l
```

# git clone git pull

#### βρισκω ενα ρεπο που θελω να κανω clone
#### παιρνω το https του
```bash
git clone "https://github.com/stavros1samaras/-TypeScript-cheatsheet-.git"
```

#### τσεκαρω το branch που βρισκομαι και αμα θελω δημιουργω καινουργιο
#### κανω αλλαγες στο remote repo
#### ζηταω τις αλλαγες που εγιναν στο remote repo
```bash
git git pull origin main ή git pull --rebase ή git pull
```


