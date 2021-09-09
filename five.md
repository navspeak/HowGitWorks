# History & Content
```                 /------>(Blob1)
(commit1) --> (Tree1) 
    |                \------>(Tree1)---->(Blob2)
    |                         /\
    \/                         |
 (commit2) --> (Tree3) ------->|
                    \
                     \--->(Blob3)
```
* Reference between commits reference history
* Others i.e. reference between commits to trees to blobs are user to track content
* Some objects like Tree1, Blob2 and Blob3 can be reached by more than one commits
* When you switch to a branch (indirectly to a commit), git forgets about other commits and updates the working area with the objects reachable from that commit only. e.g switching to branch pointing to commit 2 will make the working area look like:
```                

                           (Tree1)---->(Blob2)
                               /\
                               |
 (commit2) --> (Tree3) ------->|
                    \
                     \--->(Blob3)
```
* Merge commits are no different. Just that they have two or more parents
* Git cares about objects in .git not so much in working area although it will give a warning when overwriting a file in working area

## Fast Forward Merge - merge without Merging:
```
                 
*   6e08961 (HEAD -> main) Merge branch 'ideas'
|\
| * f93bd10 (ideas) Add tweaked apple pir receipe 2
| * 023ba36 Add tweaked apple pir receipe
* | daa1a21 Add apple pie recipe
|/
* eff0545 Add more cake
* dfc5f59 First commit

```
* git switch ideas
```
*   6e08961 ( main) Merge branch 'ideas'
|\
| * f93bd10 (HEAD ->ideas) Add tweaked apple pir receipe 2
| * 023ba36 Add tweaked apple pir receipe
* | daa1a21 Add apple pie recipe
|/
* eff0545 Add more cake
* dfc5f59 First commit

```
* git merge main (as MergedCommit has been resolved of conflicts)
```
$ git log --graph --oneline
*   6e08961 (HEAD -> ideas, main) Merge branch 'ideas'
|\
| * f93bd10 Add tweaked apple pir receipe 2
| * 023ba36 Add tweaked apple pir receipe
* | daa1a21 Add apple pie recipe
|/
* eff0545 Add more cake
* dfc5f59 First commit
```

## Losing the HEAD

* HEAD is mostly a ref a branch. Well, not always
* git switch main
```
*   6e08961 (HEAD -> main, ideas) Merge branch 'ideas'
|\
| * f93bd10 Add tweaked apple pir receipe 2
| * 023ba36 Add tweaked apple pir receipe
* | daa1a21 Add apple pie recipe
|/
* eff0545 Add more cake
* dfc5f59 First commit
```
* git checkout 6e08 => warning Detached Head
```
*   6e08961 (HEAD, main, ideas) Merge branch 'ideas'
|\
| * f93bd10 Add tweaked apple pir receipe 2
| * 023ba36 Add tweaked apple pir receipe
* | daa1a21 Add apple pie recipe
|/
* eff0545 Add more cake
* dfc5f59 First commit
```
* git branch
```
$ git branch
* (HEAD detached at 6e08961)
  ideas
  main
```
* vi recipes/apple_pie.txt and increase the number of apples and COMMIT
* vi recipes/apple_pie.txt and remove sugar and COMMIT 
```
* 0fe2e35 (HEAD) Remove sugar
* 4d8546e Add more apples
*   6e08961 (main, ideas) Merge branch 'ideas'
|\
| * f93bd10 Add tweaked apple pir receipe 2
| * 023ba36 Add tweaked apple pir receipe
* | daa1a21 Add apple pie recipe
|/
* eff0545 Add more cake
* dfc5f59 First commit
```
* Now say you want to abandon these changes and move to main
* git switch main
```
Warning: you are leaving 2 commits behind, not connected to
any of your branches:

  0fe2e35 Remove sugar
  4d8546e Add more apples

If you want to keep them by creating a new branch, this may be a good time
to do so with:

 git branch <new-branch-name> 0fe2e35

Switched to branch 'main'
```
* two of the commits are now garbage as are not pointed by a branch. This will be eventually garbage collected unless you do something like
    * git checkout 0fe2e35 (moves head to this commit)
    * git branch nouse
    * git switch main
    * or
    * git branch nouse 0fe2
```
* 0fe2e35 (HEAD -> nouse) Remove sugar
* 4d8546e Add more apples
*   6e08961 (main, ideas) Merge branch 'ideas'
|\
| * f93bd10 Add tweaked apple pir receipe 2
| * 023ba36 Add tweaked apple pir receipe
* | daa1a21 Add apple pie recipe
|/
* eff0545 Add more cake
* dfc5f59 First commit
```

## Summary
1. Current branch tracks new commits
2. Switching to another commit updates working directory
3. Unreachable objects like commits with no reference are garbage collected

