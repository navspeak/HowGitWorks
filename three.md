# Demystifying Branches:

##  BRANCH is just a REF to a COMMIT
* Rename master to main => git branch -m master main
* ls .git/refs/
```
heads/  tags/
```
* ls .git/refs/heads/
```
main
```
* cat .git/refs/heads/main
>> eff0545bff58804984535a0e0f5b33ef912e704c
* Create a new Branch viz. ideas:
  * git branch ideas
* ls .git/refs/heads/
```
main
ideas
```
* cat .git/refs/heads/ideas
>> eff0545bff58804984535a0e0f5b33ef912e704c

```
  main > eff0 < ideas
         dfc5
```
* We have two branches i.e. main and ideas pointing to same commit

## current branch
* How does git know the current branch?
  * $ cat .git/HEAD
      * ref: refs/heads/main
  * So HEAD (which is only one) is a reference to a branch
```
 HEAD > main > eff0 < ideas
               dfc5
```
* Let's add to recipes/apple_pie.txt
```
$ cat recipes/apple_pie.txt
Apple Pie

pre-made pastry
1/2 cup butter
3 tablespoons flour
1 cup sugar
8 Granny Smith apples
```
*  git add recipes/apple_pie.txt && git commit -m "Add apple pie recipe"
```
$ git log --oneline
daa1a21 (HEAD -> main) Add apple pie recipe
eff0545 (ideas) Add more cake
dfc5f59 First commit
```
* cat .git/HEAD will still be at main. But main will be a new commit
```
 HEAD > main > daa1 
               eff0 <idea
               dfc5
```
## Branching
* now "git switch idea" to make ideas the main branch
* What happened on switch?
   * Switch moves HEAD to a new branch and update working area
   * $ cat .git/HEAD
      * ref: refs/heads/~~main~~*ideas* 
```
        main > daa1 
               eff0 < idea < HEAD
               dfc5
       !! cat recipes/apple_pie.txt => the ingredients added will be gone !!
```
* Add almost same ingredients in this branch and commit
```
$ cat recipes/apple_pie.txt
Apple Pie

pre-made pastry
1/2 cup butter
3 tablespoons flour
1 cup sugar
*1 tablespoon of cinnamon*
8 Granny Smith apples
```
$ git log --oneline
```
023ba36 (HEAD -> ideas) Add tweaked apple pie receipe
eff0545 Add more cake
dfc5f59 First commit
```
```
        main > daa1      023b < idea < HEAD
                    eff0 
                    dfc5
```
      


