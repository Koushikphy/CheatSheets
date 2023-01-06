### Initial setup
```bash
git config --global user.name "User Name"
git config --global user.email "User Email"
```



### Basic commands

#### Create a new repo
```bash
git init  # initialize a folder as a git repo
git remote add origin <your_remote_repo>   # add remote origin to your repo
git branch -M main              # optional, github now uses `main` instead of `master` as the primary branch
```
or clone a repo by
```bash
git clone <your_remote_repo> # clone a repo
```

#### Stage files commit
```bash
git add .   # add files for commit
git commit -m "commit message"  # commit changes
```

#### Push commits to remote
```bash 
git push -u origin main         # push to main(or master) branch
```



### Quick one command way to add, commit and push
add this to your `~/.bashrc`
```bash
function lazygit() {
    git add .
    git commit -a -m "$1"
    git push -u origin master   # push to `master` branch, change if required
}
```
and use
```bash
lazygit "commit message"
```


### Add ssh keys to GitHub
Upload `~/.ssh/id_rsa.pub` to github ssh keys https://github.com/settings/keys. This is optional but highly recommended to authenticate remote repo with ssh keys



### .gitignore files
Files and folders listed in the file `.gitignore` will simply be, as the name suggests, ignored by git. `.gitgnore` files can be used on a repo basis or globally. Files that never should be tracked by git (e.g. security keys), are better to put in a global `.gitignore` file. The following command sets `~/.gitignore` file as a global gitignore file 
```bash
git config --global core.excludesFile '~/.gitignore'
```
<details>	
<summary> Sample global gitignore file</summary> 
.env  
dist/  
node_modules/  
*.exe  
*.mod  
*.smod  
*.o  
*.pyc  
*.so  
*.out  
*.i90  
*.swp  
.hidden  
*.aux  
*.bbl  
*.log  
*.blg  
*.out  
*.synctex.gz  

</details>   






### Remove an already tracked file from the history
```bash
git rm --cached giant_file
git commit --amend -CHEAD
git push
```

### git squash
Squash last 10 commits, choose what to `pick` and what to `squash`
```bash
git rebase -i HEAD~10
git push --force origin <branch>  # if already pushed , force to origin
```

### Signing commits
This is not necessary but recommended to sign your commits before pushing to remote. It adds an extra layer of verification that the commit was made by you. Before version 2.34, only gpg keys could be used to sign commits, but now ssh keys can be used as well. For this upload your ssh keys to Github
```bash
git config --global gpg.format ssh
git config --global user.signingkey /PATH/TO/.SSH/KEY.PUB
```

### Tags
```bash
git tag <tag_name>              # create local tag
git push origin <tag_name>      # push local tag to remote
git tag -d <tag_name>           # delete local tag
git push --delete origin <tag_name> # delete remote tag
```