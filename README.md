# version-control
Completed FrontendMasters's wonderful course "Everything you'll need to know about GIT", held by The Primeagen. 
https://frontendmasters.com/courses/everything-git/  
This repository serves as a notebook for course-related notes and an enviroment for practicing skills with Git and Github.  
In the style of "Learn in public" this repository's branches also contain experimental attempts and unsuccessful trials.  
The goal is also to keep track of things that are still unclear.   
Certificate for the course completion can be found further down. 

## Concepts
### 1. Merge (fast-forward) 
Two branches, only the other one diverges. 
Best common ancestor is the tip of the  main branch, so new commits will be placed on top of that without a merge commit (fast forward). 
- On branch main: git merge foo
```plaintext
foo             B - C  
              /        =>   A - B - C
main        A              
```
### 2. Merge (with merge commit, no conflict)
Two branches, both diverge on different files/lines.
Best common ancestor exists, a merge commit will be created and it will have two parents, one from each branch.
- On branch main: git merge foo
```plaintext
foo             B - C           B - C 
              /         =>    /       \
main        A - D - E       A - D - E - (merge commit)
```
### 3. Rebase
Moves foo to point to the latest commit on main
- **Do not rebase on public branches, only on private**
- On branch foo: git rebase main
- if need to push to remote repo: git push --force

```plaintext
foo            B - C                  B - C
             /         =>           /
main        A - D - E      A - D - E
```

## Memos
### Basics
**A commit**  
	- is a point in time representing the project in its entirety.   
	- Entiry project can be reconstructed from a single commit, representing project's state in commit's point in time.  

**Staging area / index**  
	- you add files to index,i.e. collect files together you wish to include in a commit.  

**sha**  
- secure hash algorithm, built from the content of the object. Used as identifier for commit-objects, tree-objects and blob-objects.

**Squash**  
- take several commits and turn it into one commit.  

**Best common ancestor / merge base**
- the first in common commit

**.git folder**  
Holds all of git's history. Sha's can be found in .git/objects. First 2 letters as a directory, remaining 38 as a file.  
``` git cat-file -p <sha>```, to echo out the content of:  
- commit object: holds metadata, commit message, tree-object, parent
- tree-object: directory structure at the moment of the commit, holds blobs and trees
- blob-object: a file, holds actual content of a file  

Branches are stored in: .git/refs/heads/ a branch is also just a sha.
Logs are stored in: .git/logs/HEAD

**HEAD**  
Just a pointer that points to what ever you are currently using.   
Think of a playhead on a recorder.  

**REFLOG**  
Shows where the HEAD has been.  
Excercise:  
- Create a branch and one commit in a new file
- Delete the branch: ```git branch -D <branch>```
- Use git reflog to find the commit-object, 
- ```git cat-file -p <commit-object sha>```
- ```git cat-file -p <tree-object sha>```
- ```git cat-file -p <blob-object sha> >> recoveredfile.md```
- (easier way: cherry-pick)

**Cherry Pick**  
Cherry pick the change the given commit introduces.  
Working tree must be clean before starting.  
- ```git cherry-pick <sha>```  

**Stash**  
When you have untracked changes and need to pull from remote
- ```git stash -m "msg"```
- ```git stash list```
- ```git pull```
- ```git stash pop```

### Resolving conflicts
git pull --no-rebase (git config pull.rebase false): merge and resolve conflicts manually if any  
- this will create a merge commit, which will have two parents

git pull --rebase (git config pull.rebase true): rebase and resolve conflicts manually if any  
- rebases local commits on top of the remote changes, rewrites commits history

git pull --ff-only (git config pull.ff only): fails if divergents changes, no merge or rebase will occur  

## Key takeaways
Commit's (size&quality&messages) are very important. It is easier to fix things later (inevitable) when commits are done properly.  

## Questions
The Primeagen about rebasing:  
"Likes to rebase when pulling in from remote.  
- A long lived branch with a lot of merge commits is much more difficult to revert
- Prefers to test his changes against the current state of master not against the current state he has fetched."  


![image alt](https://github.com/vesalukkarila/version-control/blob/97284d209e04c130b65e94434aec72ae1facba7c/certificate.png)  
