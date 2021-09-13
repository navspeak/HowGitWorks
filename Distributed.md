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
* See that main locally points to the new commit. Origin does not know about it yet and points to the old commit
```
$ git show-ref main
e4ff4732b3e6b45d1e9db8c6d09ad0bdd1ef32e1 refs/heads/main
30424b937aec795ed2a782eee7b149417e619407 refs/remotes/origin/main
```
* NOTE: You can't push directly to a non-bare repository (github is a bare directory with no working tree. However your local repository folder is non-bare as it has a working tree)
* git push
$ git show-ref main
```
e4ff4732b3e6b45d1e9db8c6d09ad0bdd1ef32e1 refs/heads/main
e4ff4732b3e6b45d1e9db8c6d09ad0bdd1ef32e1 refs/remotes/origin/main
```

## Pull = git fetch + merge
```
Remote
             [Main]
             o 
 ========
Local

             [Main]
             o
             [origin/main]
```
* Added one commit
```


Remote
             [Main]
             o 

Local

                               [Main]
             o  <--------------- D
             [origin/main]
```

* and Pushed
```
Remote
                             [Main]
             o  <------------ D

Local

                               [Main]
             o  <--------------- D
                               [origin/main]
```                               

* All fine till here, but if someone pushed before we could = Conflict

```
Remote
                              [Main]
             o <---------------- 8

Local

                               [Main]
             o  <--------------- D
             [origin/main]
```

* Option 1 : git push -f (not recommended)
```

Remote
                    /----8 (garbage collected eventually)
                o                 [Main]
                 <---------------- D

Local

                               [Main]
             o  <--------------- D
                        [origin/main]
```             

* Option 2: Better: Resolve conflict locally: 

        * Git fetch
```
Remote
                              [Main]
             o <---------------- 8

Local                         [origin/main]
                 <---------------8
             o                  [Main]
                 <--------------- D
```
        * Git Merge:
```
Remote
                              [Main]
             o <---------------- 8
Local
                          [origin/main]
                 <---------------8
             o                             D8 [Main]
                 <--------------- D
```             

        * Git push
```        
Remote
                          
                 <---------------8   
             o                             D8 [Main]
                 <--------------- D
             

                                             [origin/main]
                 <---------------8   
             o                             D8 [Main]
                 <--------------- D
```             

