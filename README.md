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
* git reset HEAD <one_specific_file>: Unstage a specific file
   * This will move that file from HEAD commit to the index area as it is a mixed commit.
   * This means if that specific file will only be unstanged
   * Reset with path does not take --hard. i.e. git reset --hard HEAD x.txt is not allowed.
   * To do so we use "checkout"
   
## Git checkout 
* Git checkout normally moves HEAD in the repository to a the commit hash or branch, and copies the files to working area
* _Git checkout HEAD x.txt_ => will copy x.txt from repository to working area
   * use with caution as you get no warning
   
 
# [Stash](https://www.atlassian.com/git/tutorials/saving-changes/git-stash): clipboard for your working area
* git stash --include-untracked (use this option if you want to stash unstaged file)
* You can stash partially using git stash -p (--patch)
* git stash clear
* git fsck --unreachable (fsck = file system check)


 * How does GIT know about merge conflicts => 
      * .git/MERGE_HEAD => contains temporary hash needed to merge. Points to tip of the branch we are merging. .git also has MERGE_MODE, MERGE_MSG
 * Committing parts of a file: git add | checkout | stash | reset --patch (press ? to get help)
 * git switch and restore => experimental
   * git switch ~ git checkout branch
   * git restore ~ git checkout Hash
      * git restore --staged file => to unstage
   
  ## Examining History:
   * git log --oneline --graph --decorate
   * git show COMMIT_HASH | HEAD | BRANCH
   * git show HEAD^ => parent commit of HEAD | HEAD^^ => parent of Parent of HEAD 
   * HEAD^^ = HEAD~2 (go to head and move two commits down)
   * what if it has two parents:
      * HEAD~2^2 = D
   ```
        HEAD
         A
         B
     C       D
   ```
  * git show HEAD@{"1 month ago"}
  * git blame <path_of_file>
  * git diff HEAD HEAD~2 or git diff Branch1 Branch2
  * git log
      * git log --patch
      * git log --grep apples --oneline
      * git log -Gapples --patch
      * git log HEAD~5..HEAD^ --oneline (specify oldest commit first but in output oldest commit is at top)
      * List commits in main branch but not in branch1
   ```
   $ git log branch1..main --oneline
      50a37c1 (origin/main, origin/HEAD, main) Nav in Branch1 change (#1)
   ```
  # Fixing History
   
   
