# GIT is a stupid Content tracker
```
$ cd cookbook
$ cmd //c tree //a //f
	C:.
	|   menu.txt => Apple Pie
	|
	\---recipes
			apple_pie.txt => Apple Pie
			README.txt => Put your recipes in this directory, one recipe per file.
 ```
* git status => see that files are not staged => git add *
* git commit -m "First commit" => dfc5f59a55074d6046de79f54725779e4ec193cf
* git log 
```
		commit dfc5f59a55074d6046de79f54725779e4ec193cf (HEAD -> master)
		Author: Nav <navneet.sahay@gmail.com>
		Date:   Wed Sep 8 12:55:49 2021 -0400

		First commit
 ```
* ls .git/objects/
```
		23/  36/  3e/  be/  df/  info/  pack/
```
* git cat-file dfc5f59a55074d6046de79f54725779e4ec193cf -t => commit   
* git cat-file dfc5f59a55074d6046de79f54725779e4ec193cf -p
```
		tree be4d5bfce489a2591e7fed5c672f9e52cd695a43
		author Nav <navneet.sahay@gmail.com> 1631120149 -0400
		committer Nav <navneet.sahay@gmail.com> 1631120149 -0400

		First commit
```
* git cat-file be4d5bfce489a2591e7fed5c672f9e52cd695a43 -t => tree
* git cat-file be4d5bfce489a2591e7fed5c672f9e52cd695a43 -p
```
		100644 blob 23991897e13e47ed0adb91a0082c31c82fe0cbe5    menu.txt
		040000 tree 3ee76fde69b730530f1682f1f51789e89cf30500    recipes
```  
* git cat-file 3ee76fde69b730530f1682f1f51789e89cf30500 -p
```
		100644 blob 361af858632ee7d8d8f9c4022ccaf61fc8d4799c    README.txt
		100644 blob 23991897e13e47ed0adb91a0082c31c82fe0cbe5    apple_pie.txt
```
* git cat-file 361af858632ee7d8d8f9c4022ccaf61fc8d4799c -t => blob
* git cat-file 361af858632ee7d8d8f9c4022ccaf61fc8d4799c -p => 	Put your recipes in this directory, one recipe per file.

## Object Graph
```
                                   ----> [menu.text]--->(2399) [blob|Apple Pie]
                                  /                                     /\
                                 /                                       |
(dfc5)[commit] --[./]-->(be4d)--+                                        | 
                                 \                                       |
                                  \----> [recipes/]--->(3ee7)[tree] ---- +
                                                                         |
                                                                         ---------[README.txt]------->(361a) [blob|Put your recipes...]
```
## Add one commit
* echo "Cheesecake" >> menu.txt 
* git log
```
		commit eff0545bff58804984535a0e0f5b33ef912e704c (HEAD -> master)
		Author: Nav <navneet.sahay@gmail.com>
		Date:   Wed Sep 8 13:26:42 2021 -0400

			Add more cake

		commit dfc5f59a55074d6046de79f54725779e4ec193cf
		Author: Nav <navneet.sahay@gmail.com>
		Date:   Wed Sep 8 12:55:49 2021 -0400

			First commit
 ```
* git cat-file eff0545bff58804984535a0e0f5b33ef912e704c -p
```
		tree 6ee0cdeefafa85f8baea117d3181e873e634093d
		parent dfc5f59a55074d6046de79f54725779e4ec193cf
		author Nav <navneet.sahay@gmail.com> 1631122002 -0400
		committer Nav <navneet.sahay@gmail.com> 1631122002 -0400
```
>> NOTE: except first commit, all commits have parents
* git cat-file 6ee0c -p
```
		100644 blob f1fe985b46ca38f32d7bf4024a9218cb58be74f7    menu.txt
		040000 tree 3ee76fde69b730530f1682f1f51789e89cf30500    recipes
    NOTE menu.txt file has a new hash, but recipes is same as it has not changed
```
* git cat-file f1fe -p
```
		Apple Pie
		Cheesecake
````

## New Object Graph
		
```
                                         ----> [menu.text]--->(f1fe) [blob|Apple Pie\n Cheese cake]
                                        |
(eff0)[commit] --[./]-->(6ee0)[tree] ---+
                                        |
                                        ---[recipes/]----(CONNECT TO 3ee7 below)----->             
		 
                                    ----> [menu.text]--->(2399) [blob|Apple Pie]
                                  /                                     /\
                                 /                                       |
(dfc5)[commit] --[./]-->(be4d)--+                                        | 
                                 \                                       |
                                  \----> [recipes/]--->(3ee7)[tree] ---- +
                                                                         |
                                                                         ---------[README.txt]------->(361a) [blob|Put your recipes...]  
(myTag) --> (eff0) ---> (dfc5)                                                                         
                                                                         
```                                                                         
* Here 2399 and 3ee7 are two blobs for menu.txt over two commits. It's ok to create new blobs for each change per commit for same file, but it may get too unruly with many objects for huge files. 
* git count-objects =>		8 objects, 32 kilobytes
* Git optimizes this by saving only difference, and/or compressing. That's where info and pack directories are used.
*  ls .git/objects/
    * 23/  36/  3e/  6e/  be/  df/  ef/  f1/  __info/__  __pack/__

* We may also have "Annotated Tags" pointing to a commit.
## Git Objects:
* Blobs, commits, trees, annotated tags
## What Git Really is: 
* Persited Map, stupid tracker but basically a versioned File System => Distributed Version Control System

