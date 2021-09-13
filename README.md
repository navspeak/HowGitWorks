# What is GIT?
* Persistent Map
* Stupid Content Tracker
* [Distributed] Revision Control System
# Four areas
* Stash | Working area | Index | Repository
    * .git = repository | .git/objects = object database = blobs/treers/commits = immutable, linked as Graph
    * index = staging area. If git status shows clean it means work area, index and repo are in sync
* git add => adds to index
* git diff --cached => diff between index and repository
* git rm <filename> => without option gives error
  * --cached to keep the file in working area
  * can do: git rm --cached followed by rm to remove from staging and working area. You could also use -f option
  * unstage = git rm --cached
* Move Left -> Right: add, commit
* Right to left -> git checkout
* rename: rename plus  git add or simply git mv

# Git Reset
* git commands like commit, merge, rebase, pull etc implicitly move a branch, but in that course creates new commit. Git reset is a specialized command to move the branch
* Note: git switch or git checkout change the current branch; they don't move branches
* git reset HASH 
  1. moves branch to a commit
  2. depending on options moves data to different area
    * --mixed: default => moves from Repository to only the index
    * --hard => moves to both index and working area
  
 ## Head Reset
 ```
 Working area          Index                Repository
  A'                     A'                HEAD-> Main ->(0ab) ---> A
  B                      B                                          B
 ```
 * In above example we have staged a change, so we can do:
    * git reset HEAD to unstage it (~git rm --cached)
    * git reset --hard HEAD to unstage and remove that from working area too
 
# Stash: clipboard for your working area
* git stash --include-untracked (use this option if you want to stash unstaged file)
   
