# Git

## Tutorial

* https://elmah.ir/post/118-چطور-تقریباً-هر-چیزی-را-در-git-به-حالت-قبلی-برگردانیم-قسمت-اول/

## Github Search tricks

* In Name, In Description, and In README

```
in:name spring cloud
in:description spring cloud
in:readme spring cloud

stars:>=3000 spring cloud
forks:10..20 spring cloud

language:java

user:joshlong spring cloud

org:spring-cloud spring cloud
```

## Rm Cache

```shell
git update-index --assume-unchanged <file>
# or remove them from repository by
git rm --cached file.md
git rm -r --cached /folder
```

From <https://stackoverflow.com/questions/1818895/keep-ignored-files-out-of-git-status/36877483> 

## Update fork

```shell
git remote add upstream original_git_address.git
git fetch upstream 
git pull upstream master
```

## Tags

```shell
git tag //shows all tags
git tag tagName //to tag last commit
git checkout tagName //to jump to the tagName
```