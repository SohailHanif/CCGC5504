# CCGC5504 Repo

This repo will contain code snippets and files for CCGC5504

# Commands

## Git
### First time using Git 
```
git config --global user.name "YOUR_NAME"
git config --global user.email "YOUR_EMAIL"
```

### Creating new repo 
```
git init
git remote add origin GITHUB_REPO_URL
```

### When making changes (Most Used) 
```
git add .
git commit -m "commit message"
git push origin master
git pull origin master
```

### Adding new feature that want to seperate from main code until it is finished
```
git branch NEW_BRANCH_NAME
git checkout NEW_BRANCH_NAME
git push origin NEW_BRANCH_NAME
```


### When feature done and ready to merge to main branch
```
git checkout master
git merge NEW_BRANCH_NAME
git push origin master
```