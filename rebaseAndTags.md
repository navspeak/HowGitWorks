## Let's have two branches : main & sphagetti
```
                                                            (G) < MAIN
  MAIN > (A)     (C) < SPHAGETTI   = MERGE =>           (A)     (C) <SPHAGETTI
         (B)     (D)                                    (B)     (D)
             (E)                                            (E)
             (F)                                            (F)

```
## REBASE
    * say are on Sphagetti branch, and rebase main 
      * It means the base of Sphagetti will rebase to main i.e. change from (E) to the commit pointed by MAIN i.e. (C) 
      * Note this will involve changing parents, so new commits are created
```

         (D') < SPHAGETTI
         (C')                                                 
  MAIN > (A)                       (C) <- unreachable now, garbage collected
         (B)                       (D)                                    
             (E)                                            
             (F)                                            

```
## concreate example
```
$ git log --graph --oneline
* f918158 (HEAD -> main) Tweaked again
*   6e08961 (ideas) Merge branch 'ideas'
|\
| * f93bd10 Add tweaked apple pir receipe 2
| * 023ba36 Add tweaked apple pir receipe
* | daa1a21 Add apple pie recipe
|/
* eff0545 Add more cake
* dfc5f59 First commit
```
* git checkout eff0545
* git branch sphagetti
* git switch sphagetti
* Add few commits
```
>>>  * 5cb6872 (HEAD -> sphagetti) Sphagetti second
>>>  * ca7fa8e Sphagetti initial <<<
     * eff0545 Add more cake
     * dfc5f59 First commit
```
* git rebase main
  * Successfully rebased and updated refs/heads/sphagetti.
```
Note the changed commits for Sphagetti initial & Sphagetti second
---
* 30424b9 (HEAD -> sphagetti) Sphagetti second
* ce379bc Sphagetti initial
* f918158 (main) Tweaked again
*   6e08961 (ideas) Merge branch 'ideas'
|\
| * f93bd10 Add tweaked apple pir receipe 2
| * 023ba36 Add tweaked apple pir receipe
* | daa1a21 Add apple pie recipe
|/
* eff0545 Add more cake
* dfc5f59 First commit
```

* Now we can change the base of main to sphagetti which will be a fast fwd merge (in fact could have used merge too)
  * git switch main
  * git rebase sphagetti
    * Read this as "Take Main branch and change its base to Sphagetti"
>> Rebase will take the current branch and change its base to the specified branch. In this process it will refactor history by creating new commits 

## Tag
* Annotated tag - is a database object like commit, blob and tree
  * git tag rel_1 -a -m "First release"
    * we can later do git checkout rel_1 (not switch)
    * here this is more than label, it contains metadata 
    ```
    $ ls .git/refs/tags/
      rel_1
    ```
    ```
      $ cat .git/refs/tags/rel_1
      80d46da3cb2fb7b2c0063fe436ea17f18b253b62

      $ git cat-file -t 80d46
      tag
      $ git cat-file -p 80d46
        object 30424b937aec795ed2a782eee7b149417e619407
        type commit
        tag rel_1
        tagger Nav <navneet.sahay@gmail.com> 1631297236 -0400

        First release
    ```
    
    ```
      Annotated_tag  > (80d46) > (3042) < Branch < HEAD
                                 (ce379bc)
    ```
* Lightweight tag
  * git tag dinner
  * ls .git/refs/tags/ => dinner  rel_1
  *  cat .git/refs/tags/dinner
    * 30424b937aec795ed2a782eee7b149417e619407
    * Note this is directly the commit pointed by the branch
    * In case of annotated tag it is new Object SHA1
    ```
                  Lightweight_tag   > (3042) < Branch < HEAD
                                    (ce379bc)
    ```
* Annotated tag is like a branch that points to a Tag object which points to a commit
* Lightweight tag directly points to a commit. They are almost identical to a branch, just that they don't move.
