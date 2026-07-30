# WF: Create local backup 

To point your active working repository to your new local bare repository and push all of your changes, follow these step-by-step commands:

## 1. Navigate tot project directory
Open your terminal and navigate to your local Git project directory.
```
cd /c/myrepo
```
## 2. Verify remote url
Check your current remote URL (usually named origin) to see where it currently points:
```bash
git remote -v
```

## 3. Create a local git repo in parallel folder or in parent
```bash
mkdir [backup.git]
cd [backup.git]
git init --bare

# Important: Point HEAD to your actual default branch (e.g., main)
git symbolic-ref HEAD refs/heads/main
```

## 4. Change the remote URL to your new existing repository or 
```bash
git remote set-url origin [path-to/local-repo-name.git]
# example /c/myrepo/local-repo-name.git
```

## 4. Add a backup repository:
If you want to keep the `origin` and add another backup you can do
```bash
git remote add backup [/path/to/your/backup.git]]
```

## 5. Verify the change 
Ensure the URL has updated correctly
```bash
git remote -v
# it will print the new location of origin
```

## 6. Push Your Local Code (If Needed)
If your new existing repository is completely empty and you want to push all of your existing local branches and tags to it, execute the following commands
```bash
# Push master branch
git push backup master

# Push all local branches
git push backup --all

# Push all tags
git push backup --tags
```
