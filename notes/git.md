# Git

### Rm Cache
```shell
git update-index --assume-unchanged <file>
# or remove them from repository by
git rm --cached file.md
git rm -r --cached /folder
```

From <https://stackoverflow.com/questions/1818895/keep-ignored-files-out-of-git-status/36877483> 

### Update fork

```
git remote add upstream original_git_address.git
git fetch upstream 
git pull upstream master
```