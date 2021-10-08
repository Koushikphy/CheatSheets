
##### Initial setup
```bash
git config --global user.name "User Name"
git config --global user.email "useremail"
```
#### Add ssh keys to github
upload `~/.ssh/id_rsa.pub` to github ssh keys



#### Basic commnads
```bash 
git init  # inititalize a folder as a git repo
git remote add origin git@github.com:<your_repo>   # add remote origin to your repo
git clone <your_repo> # clone a repo
git add .   # add files for commit
git commit -m "commit message"  # commit changes
git branch -M main              # optional, github now uses `main` instead of `master` as primary branch
git push -u origin main         # push to main(or master) branch
```


#### Quick one commnad way to add, commit and push
add this to your `~/.bashrc`
```bash
function lazygit() {
    git add .
    git commit -a -m "$1"
    git push -u origin master   # push to `master` branch, change if required
}
```
and use
```bash
lazygit "commit message"
```



#### Remove a already tracked file from history
```bash
git rm --cached giant_file
git commit --amend -CHEAD
git push
```