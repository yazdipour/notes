# Git

- [I Code Dis./Discover Github Repo](http://icodedis.tool.cards/)
- http://shields.io/
- http://jlord.us/git-it/
- http://ohshitgit.com/
- [Download Github Folder](https://minhaskamal.github.io/DownGit/#/home)
- [GitZip for github Extension](https://chrome.google.com/webstore/detail/gitzip-for-github/ffabmkklhbepgcgfonabamgnfafbdlkn?hl=en)

## GitFlow

![GitFlow](assets/git-flow.png)

## Doc

- https://docsify.js.org/
- https://github.com/pedronauck/docz
- https://www.gitbook.com

## Tutorial

- https://elmah.ir/post/118-چطور-تقریباً-هر-چیزی-را-در-git-به-حالت-قبلی-برگردانیم-قسمت-اول/

## Github Search tricks

- In Name, In Description, and In README

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

## Crypt

https://www.freecodecamp.org/news/how-to-securely-store-api-keys-4ff3ea19ebda/

### git-remote-gcrypt

The first solution lets you encrypt a whole Git repository. git-remote-gcrypt does that by adding functionality to Git remote helpers so that a new encrypted transport layer becomes available. Users only have to set up a new encrypted remote and push code into it.

### git-secret

git-secret is a tool that works on your local machine and encrypts specific files before you push them to your repository. Behind the scenes, git-secret is a shell script that uses GNU Privacy Guard (GPG) to encrypt and decrypt files that might have sensitive information.

### git-crypt

Another solution is git-crypt. It is very similar to git-secret in the way it operates, but it has some interesting differences.

The first thing to notice about git-crypt is that it is a binary executable and not a shell script, as git-secret is. Being a binary executable means that to use it you first have to compile it, or you need to find a binary distribution for your machine.
