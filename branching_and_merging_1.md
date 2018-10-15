# Branching and merging I

## Create and checkout a branch. 

Use `git branch` to verify that you have a single branch in your local repository named `master. Use `git log --oneline --graph` to verify that you are currently on the most recent commit. You should see `HEAD -> master` on the most recent commit

```
projecta$ git branch
* master
projecta$ git log --oneline --graph
* 5d430e4 (HEAD -> master, tag: v0.1, origin/master) add README.md
* d196262 add fileA.txt
```

Create and checkout a branch off the latest master commit named "featureX".

```
projecta$ git branch featureX
projecta$ git branch
  featureX
* master

projecta$ git checkout featureX
Switched to branch 'featureX'

projecta$ git branch
* featureX
  master

projecta$ git log --oneline --graph
* 5d430e4 (HEAD -> featureX, tag: v0.1, origin/master, master) add README.md
* d196262 add fileA.txt
```

## Create commits on the branch.

Now that you have created and checked out the `featureX` branch, you can do some work on the project without affecting the `master` branch. Create a commit on the `featureX` branch.
```
projecta$ echo "feature mistake" >> fileA.txt 
projecta$ git add fileA.txt
projecta$ git commit -m "add feature mistake"
[featureX 4800e6f] add feature mistake
 1 file changed, 1 insertion(+)

projecta$ git log --oneline --graph
* 4800e6f (HEAD -> featureX) add feature mistake
* 5d430e4 (tag: v0.1, origin/master, master) add README.md
* d196262 add fileA.txt
```

Execute `checkout master` to checkout the master branch. Your working tree will be updated with the older version of `fileA.txt`. 

```
projecta$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

projecta$ cat fileA.txt
projecta$ 
```

Execute `git log --oneline --graph`. Only information about the current branch is listed. 
```
projecta$ git log --oneline --graph
* 5d430e4 (HEAD -> master, tag: v0.1, origin/master) add README.md
* d196262 add fileA.txt
```

Execute `git log --oneline --graph --all` Add `--all` shows all of the local branches. 
```
projecta$ git log --oneline --graph --all
* 4800e6f (featureX) add feature mistake
* 5d430e4 (HEAD -> master, tag: v0.1, origin/master) add README.md
* d196262 add fileA.txt
```

Change back to the `featureX` branch and create another commit on it. 
```
projecta$ git checkout featureX
Switched to branch 'featureX'

projecta$ echo "feature mistake 2" >> fileA.txt 
projecta$ cat fileA.txt 
feature mistake
feature mistake 2

projecta$ git add fileA.txt 
projecta$ git commit -m "add feature mistake 2"
[featureX edee88e] add feature mistake 2
 1 file changed, 1 insertion(+)

projecta$ git log --oneline --graph --all
* edee88e (HEAD -> featureX) add feature mistake 2
* 4800e6f add feature mistake
* 5d430e4 (tag: v0.1, origin/master, master) add README.md
* d196262 add fileA.txt
```

## Checkout an old commit.

Let's say you want to view the first change that we made on the `featureX` branch. Checkout the first commit you made on the `featureX` branch ("add feature mistake") by executing `git checkout HEAD~`. The appended ~ means "parent of the commit". Git will warn you that you are entering a detached HEAD state because your HEAD reference points directly at the SHA-1 of a commit, instead of to a branch label.

```
projecta$ git checkout HEAD~
Note: checking out 'HEAD~'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by performing another checkout.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -b with the checkout command again. Example:

  git checkout -b <new-branch-name>

HEAD is now at 4800e6f add feature mistake 

projecta$ git log --oneline --graph --all
* edee88e (featureX) add feature mistake 2
* 4800e6f (HEAD) add feature mistake
* 5d430e4 (tag: v0.1, origin/master, master) add README.md
* d196262 add fileA.txt
```

## Delete a branch.

Try to delete the `featureX` branch using `git branch -d featureX`. You will see that Git won't let you delete this branch, because it has not been merged. Your two comiits on the `featureX` branch would become "dangling commits" and would eventually be garbage-collected by Git. 
```
projecta$ git checkout master
Previous HEAD position was 4800e6f add feature mistake
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

projecta$ git branch -d featureX
error: The branch 'featureX' is not fully merged.
If you are sure you want to delete it, run 'git branch -D featureX'.
```

If you are sure that you want to delete this branch, use the `-D` option with `git branch` command.

``` 
projecta$ git branch -D featureX
Deleted branch featureX (was edee88e).

projecta$ git log --oneline --graph --all
* 5d430e4 (HEAD -> master, tag: v0.1, origin/master) add README.md
* d196262 add fileA.txt
```


## Perform a fast-forward merge.

Let's assume that feature2 branch is ready to be merged into the `master` branch. Start by checking out the `master` branch with `git checkout` command. 
```
projecta$ git log --oneline --graph --all
* 1fb2939 (HEAD -> feature2) add feature2
* 0e7edd8 (origin/master, master) add feature 1
* 5d430e4 (tag: v0.1) add README.md
* d196262 add fileA.txt

projecta$ git checkout master
Switched to branch 'master'
Your branch is up to date with 'origin/master'.

projecta$ git log --oneline --graph --all
* 1fb2939 (feature2) add feature2
* 0e7edd8 (HEAD -> master, origin/master) add feature 1
* 5d430e4 (tag: v0.1) add README.md
* d196262 add fileA.txt
```

Execute `git merge feature2`. By default, this command will perform a fast-forward merge if possible. Executing `git log --oneline --graph --all` command will show you a linear history with the `master` and `feature2` labels on the most recent commit. The fast-forward merge simply moves the `master` branch label to the latest commit.
```
projecta$ git merge feature2
Updating 0e7edd8..1fb2939
Fast-forward
 fileA.txt | 1 +
 1 file changed, 1 insertion(+)

projecta$ git log --oneline --graph --all
* 1fb2939 (HEAD -> master, feature2) add feature2
* 0e7edd8 (origin/master) add feature 1
* 5d430e4 (tag: v0.1) add README.md
* d196262 add fileA.txt
```

Delete the `feature2` branch label.
```
projecta$ git branch -d feature2
Deleted branch feature2 (was 1fb2939).
projecta$ git log --oneline --graph --all
* 1fb2939 (HEAD -> master) add feature2
* 0e7edd8 (origin/master) add feature 1
* 5d430e4 (tag: v0.1) add README.md
* d196262 add fileA.txt
```

## Perform a merge with a merge commit.

This time, when you are ready to merge in the `feature3` branch, execute `git merge --no-ff feature3` (do not forget to checking out the `master` branch first). The `--no-ff` option will create a merge commit, resulting in a non-linear history.
```
projecta$ git log --oneline --graph --all
* 56cea6d (HEAD -> feature3) add feature3
* 1fb2939 (master) add feature2
* 0e7edd8 (origin/master) add feature 1
* 5d430e4 (tag: v0.1) add README.md
* d196262 add fileA.txt

projecta$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits

projecta$ git log --oneline --graph --all
* 56cea6d (feature3) add feature3
* 1fb2939 (HEAD -> master) add feature2
* 0e7edd8 (origin/master) add feature 1
* 5d430e4 (tag: v0.1) add README.md
* d196262 add fileA.txt

projecta$ git merge --no-ff feature3
Merge made by the 'recursive' strategy.
 fileA.txt | 1 +
 1 file changed, 1 insertion(+)

projecta$ git log --oneline --graph --all
*   25fafa7 (HEAD -> master) Merge branch 'feature3'
|\  
| * 56cea6d (feature3) add feature3
|/  
* 1fb2939 add feature2
* 0e7edd8 (origin/master) add feature 1
* 5d430e4 (tag: v0.1) add README.md
* d196262 add fileA.txt
```

Delete the `feature3` branch label
```
projecta$ git branch -d feature3
Deleted branch feature3 (was 56cea6d).

projecta$ git log --oneline --graph --all
*   25fafa7 (HEAD -> master) Merge branch 'feature3'
|\  
| * 56cea6d add feature3
|/  
* 1fb2939 add feature2
* 0e7edd8 (origin/master) add feature 1
* 5d430e4 (tag: v0.1) add README.md
* d196262 add fileA.txt
```


