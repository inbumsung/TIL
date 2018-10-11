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


> To be uploaded
 
