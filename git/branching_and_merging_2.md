# Branching and merging II

## Create branches that contain a merge conflict. 

Create a local repository named `projectd`.
```
repos$ mkdir projectd
repos$ cd projectd
projectd$ git init
Initialized empty Git repository in /Users/inbumsung/repos/projectd/.git/
```

Create a commit in your `projectd` repository with a `fileA.txt` file containing a string "feature 1". The commit message should be "add feature 1". This commit should be on the `master` branch.
```
projectd$ echo "feature 1" > fileA.txt
projectd$ git add fileA.txt
projectd$ git commit -m "add feature 1"
```

Create and checkout a branch off of the latest master commit named "feature2".
```
projectd$ git branch feature2
projectd$ git checkout feature2
Switched to branch 'feature2'
```

In your local repository, create a commit on the `feature2` branch with the following:
- modify `fileA.txt`, adding "feature 2" directly under the line "feature 1"
- add a commit message of "add feature 2"
```
projectd$ echo "feature 2" >> fileA.txt
projectd$ git add fileA.txt 
projectd$ git commit -m "add feature2"
[feature2 afe1716] add feature2
 1 file changed, 1 insertion(+)
```

Checkout the `master` branch 
```
projectd$ git checkout master
Switched to branch 'master'
```

Create a commit on the `master` branch with the following:
- modify `fileA.txt`, adding "feature 3" directly under the line "feature 1"
- add a commit message of "add feature 3"
```
projectd$ echo "feature 3" >> fileA.txt
projectd$ git add fileA.txt
projectd$ git commit -m "add feature3"
```

## Merge the branches, resolving the merge conflict.
Verify that the `master` branch is checked out.
```
projectd$ git branch
  feature2
* master
```

Execute `git merge feature2` and attempt to merge in the `feature2` branch. You should see that there is a merge conflict.
```
projectd$ git merge feature2
Auto-merging fileA.txt
CONFLICT (content): Merge conflict in fileA.txt
Automatic merge failed; fix conflicts and then commit the result.
```

Execute `git status` to see that Git has modified `fileA.txt`.
```
projectd$ git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)

    both modified:   fileA.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

View the `fileA.txt` file. Notice the conflict markers in the file. That is the part of the merge that Git couldn't automatically resolve.
```
projectd$ cat fileA.txt 
feature 1
<<<<<<< HEAD
feature 3
=======
feature 2
>>>>>>> feature2
```

Rather than fix the conflict right now, abort the merge process by executing `git merge --abort`
```
projectd$ git merge --abort
```

Verify that you are back to the state before the merge attempt, with no uncommitted files in the working tree.
```
projectd$ git status
On branch master
nothing to commit, working tree clean
```

This time, let's resolve the merge conflict. Repeat the merge attempt. You should again see a merge conflict.
```
projectd$ git merge feature2
Auto-merging fileA.txt
CONFLICT (content): Merge conflict in fileA.txt
Automatic merge failed; fix conflicts and then commit the result.
```

Edit `fileA.txt` to resolve the merge conflict. Remove the conflict markers and make sure the file contains three lines of text: "feature 1", "feature 2" and "feature 3".
```
projectd$ cat fileA.txt 
feature 1
feature 2
feature 3
```

Add `fileA.txt` to the staging area so that the fixed version of the file is part of the merge commit.
```
projectd$ git add fileA.txt 
projectd$ git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

    modified:   fileA.txt
```

Commit the merge. Accept the default merge commit message.
```
projectd$ git commit 
[master 2ffd45c] Merge branch 'feature2'
```

After deleting the `feature2` branch label, verify that you have a commit graph with a merge commit containing all three features.
```
projectd$ git branch -d feature2
Deleted branch feature2 (was afe1716).

projectd$ git log --oneline --graph
*   2ffd45c (HEAD -> master) Merge branch 'feature2'
|\  
| * afe1716 add feature2
* | 1d03722 add feature3
|/  
* 32ec0a4 add feature 1
``` 
