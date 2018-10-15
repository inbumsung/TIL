# Starting Git with command line

## Configuring user name and email address

Configure user name and email address
```
$ git config --global user.name "Your Name"
$ git config --global user.email "your@email"
``` 

View your current setting 
```
$ git config user.name
$ git config user.email
```

List all variables set in config file, along with their values
```
$ git config --list
```

## Intitialize an empty local Git repository 
Create a repos directory (normally in user directory).
```
$ cd ~ 
~$ mkdir repos
```

In your `repos` directory, create a project directory (and it will be your local repository)
```
~$ cd repos
repos$ mkdir projecta
```

Change to your project directory and initialize a repository.
```
repos$ cd projecta
projecta$ git init
Initialized empty Git repository in projecta/.git/
```

## Commit to a local repository

View file status using `git status`. 
``` 
projecta$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)

projecta$ touch fileA.txt
projecta$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	fileA.txt

nothing added to commit but untracked files present (use "git add" to track)
```

Stage content using `git add`.
```
projecta$ git add fileA.txt
projecta$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   fileA.txt
```

Commit content using `git commit`.
```
projecta$ git commit -m "add fileA.txt" 
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 fileA.txt
projecta$ git status
On branch master
nothing to commit, working tree clean
```

View the commit history using `git log`.
```
projecta$ git log
```

## Push to a remote repository

There are two fundamental ways to start working with a remote repository. 
1. If you do not have an exisiting local repository, then you will `clone` the remote repository, creating a local repository that is associated with the remote repository.
2. If you already have a local repository with commits that you want to push to a remote repository, then you will `add` the remote repository to your local repository

Clone the remote repository with `git clone` command.
```
repos$ git clone https://bitbucket.org/atlassian_tutorial/helloworld.git
Cloning into 'helloworld'...
remote: Counting objects: 35, done.
remote: Compressing objects: 100% (21/21), done.
remote: Total 35 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (35/35), done.

repos$ cd helloworld
helloworld$ ls
LICENSE	README	pom.xml	src

helloworld$ git remote -v
origin	https://bitbucket.org/atlassian_tutorial/helloworld.git (fetch)
origin	https://bitbucket.org/atlassian_tutorial/helloworld.git (push)

```

Create a remote repository on Github named projecta.  
Then add the remote repository with `git remote add` command (from your local repository).
```
helloword$ cd~/repos/projecta/
projecta$ git remote add origin https://github.com/inbumsung/projecta.git
projecta$ git remote -v
origin  https://github.com/inbumsung/projecta.git (fetch)
origin  https://github.com/inbumsung/projecta.git (push)
```

Create a commit in the local repository.

```
projecta$ echo "projecta's README" > README.md
projecta$ git add README.md
projecta$ git commit -m "add README.md"
```

Push the commit to the remote repository. The `-u` flag sets up the local and remote branches as tracking branches. `origin` is a shortcut name for the remote repository. `master` is the branch to push.
```
projecta$ git push -u origin master
To https://github.com/inbumsung/projecta.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.

projecta$ git status
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
```

## References

Excuting the `git show` command will show the contents of the commit object, as well as some information on what has changed.
```
projecta$ git log --oneline
5d430e4 (HEAD -> master, origin/master) add README.md
d196262 add fileA.txt

projecta$ git show 5d430e4
commit d1962622ddf356df58eb6e3c72d77e6ab9afb96b
Author: Inbum Sung <mirinae145@gmail.com>
Date:   Thu Oct 11 20:47:41 2018 +0900

    add fileA.txt

diff --git a/fileA.txt b/fileA.txt
new file mode 100644
index 0000000..e69de29
```

Use the `git tag` command for attaching a version lavel to the specific commit. Create an annotated tag by specifying the -a option. Use the -m option to specify a tag message. You do not need to specify a commit, because the command ddefaults to HEAD (reference to the current commit).

```
projecta$ git tag -a -m "includes feature 1" v0.1
projecta$ git show v0.1
tag v0.1
Tagger: Inbum Sung <mirinae145@gmail.com>
Date:   Sun Oct 14 16:19:38 2018 +0900

includes feature 1

commit 5d430e4e3058627eecb01dbc10e36d50dba034b9 (HEAD -> master, tag: v0.1, origin/master)
Author: Inbum Sung <mirinae145@gmail.com>
Date:   Thu Oct 11 21:32:36 2018 +0900

    add README.md

diff --git a/README.md b/README.md
new file mode 100644
index 0000000..e69de29

projecta$ git tag
v0.1
```

Push the tag to the remote repository.
```
projecta$ git push origin v0.1
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Writing objects: 100% (1/1), 167 bytes | 167.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To https://github.com/inbumsung/projecta.git
 * [new tag]         v0.1 -> v0.1
```
