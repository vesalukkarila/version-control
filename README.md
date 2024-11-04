# version-control

## Excercises
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

```plaintext
foo            B - C                  B - C
             /         =>           /
main        A - D - E      A - D - E
```

