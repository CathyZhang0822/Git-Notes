Reference: https://willdemaine.ghost.io/a-simpler-phabricator-stacked-diff-workflow/  

## Create stacked diff
First let's create a branch and make a simple change, then commit that change:
```
✔ ~/Projects/phab/willyd [master|✔] $ arc branch willA
Branch willA set up to track local branch master by rebasing.
Switched to a new branch 'willA'
✔ ~/Projects/phab/willyd [willA|✔] $ mkdir -p stacked/simple
✔ ~/Projects/phab/willyd [willA|✔] $ vim stacked/simple/a
✔ ~/Projects/phab/willyd [willA|…1] $ git add .
✔ ~/Projects/phab/willyd [willA|●1] $ git commit -m "Create simple directory. Add initial work in a"
```

Nothing radical there. We can now ran `arc diff` like normal to create a revision:
```
✔ ~/Projects/phab/willyd [willA ↑·1|✔] $ arc diff
Created a new Differential revision:
        Revision URI: https://phab.company.com/D670

Included changes:
  A       stacked/simple/a
```
Good so far. We now want to move on to the next part of our feature while other people are reviewing that first diff.   
So now we want to make a new branch **from willA**
```
✔ ~/Projects/phab/willyd [willA ↑·1|✔] $ arc branch willB
Branch willB set up to track local branch willA by rebasing.
Switched to a new branch 'willB'
```
Note that git reports that willB is setup to track willA, not master. That is very important. Let's do some work in willB:
```
✔ ~/Projects/phab/willyd [willB|✔] $ vim stacked/simple/b
✔ ~/Projects/phab/willyd [willB|…1] $ git add .
✔ ~/Projects/phab/willyd [willB|●1] $ git commit -m "Add work in b"
[willB cebed10] Add work in b
 1 file changed, 1 insertion(+)
 create mode 100644 stacked/simple/b
 ```
 We want to diff against willA. From what I can tell, most people only ever use `arc diff` - if we did that, we'd create a diff between willB and master, 
 which would also send the changes that we made in willA
 ```
 ✔ ~/Projects/phab/willyd [willB ↑·1|✔] $ arc diff willA
Created a new Differential revision:
        Revision URI: https://phab.company.com/D671

Included changes:
  A       stacked/simple/b
 ```
 Also add `depends on D12345` in your diff's summary
 
 **Update: `arc diff` will also do. Now `arc diff parentBranch` will cause build error**
 
 ## Edit parent commits
 Switch to willA branch. Make some change. Then `git add -A` and `git commit --amend`
 Switch to master. Run `git pull`
 Switch to willA. Run `git pull --rebase origin master`
 Switch to willB. Run `git rebase`. Done.
 
 ## Land
 Follow two rules:
 1. We have to land from the bottom up.  
 2. We have to land with --keep-branch.  
 This flow is often referred to as 'stacked', but maybe 'queued' is a better explanation because our diffs are FIFO.
  **That means that we have to land willA before we land willB**.  
  Using `--keep-branch` tells are not to delete willA branch after we've landed it, which is the default behavious.  
  ```
  ✔ ~/Projects/phab/willyd [master|✔] $ git checkout willA 
Switched to branch 'willA'
Your branch is ahead of 'master' by 1 commit.
✔ ~/Projects/phab/willyd [willA ↑·1|✔] $ arc land --keep-branch
Landing current branch 'willA'.
This commit will be landed:

      - 5acd280 Create simple directory. Add initial work in a

Landing revision 'D670: Create simple directory. Add initial work in a'...
BUILDS PASSED  Harbormaster builds for the active diff completed successfully.
PUSHING  Pushing changes to "origin/master".
...
DONE  Landed changes.
```
Land child commit:   
```
git pull --rebase origin master
arc land --keep-branch
```
You can't use `arc land` or `arc land --revision D671` because diff from willB to master contains both commits.
  
