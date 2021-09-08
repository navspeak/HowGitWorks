- Plumbing vs Porcelain: https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain
- Git is a Distributed Revision Control System
- man git =		git - *the stupid content tracker*
- Git is a Persitent Map where keys are hashes and values are sequence of bytes
 ```
	$ echo "Apple Pie" | git hash-object --stdin #Plumbing command
		23991897e13e47ed0adb91a0082c31c82fe0cbe5
 ```
- For *Persitent* add -w 
```
$ mkdir howgitworks && cd howgitworks
$ git init
$ git branch -m main
$ ls -a
    echo "Apple Pie" | git hash-object --stdin -w
	  23991897e13e47ed0adb91a0082c31c82fe0cbe5
$ ls .git/objects/ => 23/  info/  pack/
$ ls .git/objects/23 => 991897e13e47ed0adb91a0082c31c82fe0cbe5 => blob
$ git cat-file 23991897e13e47ed0adb91a0082c31c82fe0cbe5 -t
		blob
$ git cat-file 23991897e13e47ed0adb91a0082c31c82fe0cbe5 -p
		Apple Pie
```
- git switch(old) vs git checkout

