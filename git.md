Config git
```bash
git config --global user.name "OrbitalOyster"
git config --global user.email "OrbitalOyster@gmail.com" 
```

Clear credentials
```bash
git config --global --unset credential.helper
```

Getting started
```bash
git init
```

Create file .gitignore, add following lines:
```
/node_modules
dist
.env
```

Check status
```bash
git status
```

Add file to staging
```bash
git add app.js
```

Add all files to staging
```bash
git add .
```

Remove file from staging
```bash
git reset app.js
```

List changes
```bash
git checkout
```

Undo changes
```bash
git checkout app.js
```

Commit
```bash
git commit -m "First commit"
```

Undo commit
```bash
git reset HEAD~
```

Check log
```bash
git log
git log --pretty=oneline
git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short
```

Go to commit
```bash
git checkout cb42912
```

Go back to top
```bash
git checkout master
```

Create branch
```bash
git checkout -b experimental_branch
```

Make branch master
```bash
git checkout master
git merge master_candidate
```
