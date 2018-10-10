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
Create a repos directory (normally in user directory)
```
$ cd ~ 
~$ mkdir repos
```

In your `repos` directory, create a project directory (and it will be your local repository)
```
~$ cd repos
repos$ mkdir projecta
```

Change to your project directory and initialize a repository
```
repos$ cd projecta
projecta$ git init
Initialized empty Git repository in projecta/.git/
```

## Commit to a local repository

> To be uploaded 
