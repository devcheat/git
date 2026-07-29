# WF: Create local backup 

To point your active working repository to your new local bare repository and push all of your changes, follow these step-by-step commands:

## 1. Open your terminal and navigate to your local Git project directory.
```
cd /c/myrepo
```
## 2.Check your current remote URL (usually named origin) to see where it currently points:
```bash
git remote -v
```

## 3. Create a local git repo in pARALLEL folder
```bash
mkdir [backup.git]
cd [backup.git]
git init --bare
```

## 4. Change the remote URL to your new existing repository using the GitHub recommended command:

### If clone
```bash
git remote set-url origin [path-to/local-repo-name.git]
# example /c/myrepo/backu
```

### If backup
If you want to keep the `origin` and add another backup you can do
```bash
git remote add backup [/path/to/your/backup.git]]
```

## 5. Verify the change to ensure the URL has updated correctly
```bash
git remote -v
# it will print the new location of origin
```

## 6. Push Your Local Code (If Needed)If your new existing repository is completely empty and you want to push all of your existing local branches and tags to it, execute the following commands
```bash
# Push master branch
git push backup master

# Push all local branches
git push backup --all

# Push all tags
git push backup --tags
```
