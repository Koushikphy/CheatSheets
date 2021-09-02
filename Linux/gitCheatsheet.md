
##### Set user information
```bash
git config --global user.name "User Name"
git config --global user.email "useremail"
```
#### Add ssh keys to github
upload `~/.ssh/id_rsa.pub` to github ssh keys


#### Remove a already tracked file from history
```bash
git rm --cached giant_file
git commit --amend -CHEAD
git push
```







