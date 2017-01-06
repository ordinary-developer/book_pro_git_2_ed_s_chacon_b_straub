Submodules
==========

Starting with Submodules
------------------------

To add a new submodule:
```
$ git submodule add <repository-address>
```
(you can add a different path at the end of the command 
 if you want it to go elsewhere).

To see a nice 'diff' output type from the root directory of the project:
```
$ git diff --cached --submodule
```


Cloning a project with Submodules
---------------------------------

#### 1-st way:
Clone the whole project:
```
$ git clone <repository-address>
```

For each submodule folder enter this folder, 
init the submodule and fetch the submodule contents
```
$ cd <submodule folder>
$ git submodule init
$ git submodule update
```

#### 2-nd way:
Clone the whole project with the '--recursive' command line argument:
```
$ git clone --recursive <repository-address>
```


Pulling in upstream changes to a submodule
------------------------------------------

To fetch from the submodule origin you can use two ways:

#### 1-st way:
in the root project directory:
```
$ cd <submodule-folder>
$ git fetch
$ git merge origin/master
```

#### 2-nd way:
in the root project directory:
```
$ git submodule update --remote <submodule-repository-name>
```

for updating all submodules:
```
$ git submodule update --remote
```

If you want to have the submodule track the othere branch (not master),
you can set it in either your '.gitmodules' file 
(so every else also tracks it),
or just in your local '.git/config' file

for the '.gitmodules' file:
from the root project
```
$ git config -f .gitmodules submodule.<SubmoduleName>.branch <branch-name>
$ git submodule update --remote
```
(if you leave '-f .gitmodules' it will only make change for you)
(example:
<SubmoduleName> - DbConnector (without brackets)
<branch-name> - stable (without brackets))

To see log for a submodule:
in the root project
```
$ git log --submodule
```


Working in a submodule
----------------------

To get data from submodule-repository:
in the submodule folder:
```
$ git checkout stable
$ git submodule update --remote --merge
```

if you already have local commits in your submodule,
then in a submodule directory:
```
$ git submodule update --remote --merge
// or
$ git submodule update --remote --rebase
```
If you have conflicts you can resolve them as usually
(if you simly try `git submodule update --remote`,
 then Git will fetch the changes 
 but not overwrite unsaved work in your submodule directory)


Publishing submodule changes
----------------------------

In the main project directory:
```
$ git push --recurse-submodules=check
```
If submodules are not pushed, 
- you can enter each submodule directory and manually push changes
- in the root director `$ git push --recurse-submodules=on-demand`  
  (here Git will try to push all submodules automatically)


Submodules tips
---------------

A 'foreach' submodule command allows to run some arbitrary command
in each submodule:
```
$ git submodule foreach 'git stash'
```

