*  git clone /c/Users/Navneet/IdeaProjects/pluralSight/howgitworks/cookbook
*  cat .git/config
```
[remote "origin"]
        url = C:/Users/Navneet/IdeaProjects/pluralSight/howgitworks/cookbook
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "main"]
        remote = origin
        merge = refs/heads/main
```
* git branch => shows only main
* Once you switch to another branch it will show up
* You may use git branch --all to get all remote and local branches
```
* main
  remotes/origin/HEAD -> origin/main
  remotes/origin/ideas
  remotes/origin/main
  remotes/origin/noyse
  remotes/origin/sphagetti
```
* .git/refs/heads => local branches
* .git/refs/remotes => remote branches
  * You may only find HEAD inside remotes/origin
      * ref: refs/remotes/origin/main
  * .git/packed-refs contains other remote branches as a part of git's low level optimization
* .git/refs/tags => local tags
* git show-ref main
```
30424b937aec795ed2a782eee7b149417e619407 refs/heads/main
30424b937aec795ed2a782eee7b149417e619407 refs/remotes/origin/main
```
* whereas since we have never switched to sphagetti locally
    * $ git show-ref sphagetti => points to only remote. Once you switch locally it will have refs to refs/head i.e. local
`       * 30424b937aec795ed2a782eee7b149417e619407 refs/remotes/origin/sphagetti

## Push
* Let's make one commit locally
```
git commit -m "Lemon juice"
[main e4ff473] Lemon juice
 1 file changed, 1 insertion(+)
```
