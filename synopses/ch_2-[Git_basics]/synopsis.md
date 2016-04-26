Git basics
==========


base
----

each file in your working directory can be in one of two states: 
tracked or untracked  
- tracked files are files that were in the last snapshot;
  they can be unmodified, modified, or staged
- untracked files are everything else - any files in your working 
  directory that were not in your last snapshot and are not in 
  your staging area

```
 unracked                unmodified          modified        staged
   |                        |                   |               |
   |                    add the file                            |
   |----------------------------------------------------------->|
   |                        | edit the file     |               |
   |                        | ----------------->|               |
   |                        |                   | stage the file|
   |                        |                   | ------------->|
   | remove the file        |                                   |       
   |<---------------------- |                commit             |
   |                        | <-------------------------------- |
```


#### git add

"git add" - is a multipurpose command - you use it to begin tracking
new files, to stage files, and to do other things like marking 
merge-conflicted files as resolved


#### git diff

to see what you've changed but not yet staged type
```git
$ git diff --color
```
this command compares what is in your working directory with what is 
in your staging area

to see what you've staged that will go into your next commit type
```git
$ git diff --staged --color
```
this command compares your staged changes to your last commit


#### git commit

to commit your changed use the command
```git
$ git commit
$ git commit --message "Commit messages"
$ git commit --all --message "Commit message"
```


#### git rm

to remove file it is not neccessary to use standard unix "rm" 
command, instead you can type

if you have not changed the file
```git
$ git rm file-to-remove
```

or if you have changed and then staged the file
```git
$ git rm --force file-to-remove
```
and then commit your changes


by the next command you can keep the file in your working tree,
but it will be untracked
```git
$ git rm --cached file-name
```
after that you must commit your changes
 

#### git mv

if you want to rename a file in Git, you can run something like
```git
$ git mv file_from file_to
```
and then you must commit your changes

this is equivalent to running something like that
```git
$ mv file_from file_to
$ git rm file_from
$ git add file_to
```


#### git log

to see your history
```git
$ git log --color
```

to see the difference introduced in each commit
```git
$ git log --patch -2 --color
```
you can use -2, which limits the output to only the last two entries

to see some abbreviated stats for each commit
```git
$ git log --stat --color
```

the option "--pretty" changes the log output to formats other 
than the default

The next option prints each commit in a single line
```git
$ git log --pretty=oneline
```

The "format" option allows you to specify your own log output format,
for example
```git
$ git log --pretty=format:"%h - %an, %ar : %s"
```

to see your commit history as a graph
```git
$ git log --graph
```

useful option - "--abbrev-commit"
shows only the first few characters of the SHA-1 checksum 
instead of all 40

another useful command
```git
$ git log --oneline --decorate --graph --color
```


#### git commit --amend

this command is useful when you commit too early and possibly forget
to add some files, or you mess up your commit message  
this command takes your staging area and uses it for the commit  
but the second commit replaces the results of the first
```git
$ git commit --message 'Initial commit'
$ git add forgotten_file
$ git commit --amend
```


#### git reset HEAD filename

this command is used to unstage the 'filename' 
but to keep it modified


#### git checkout -- filename

this commnad unmodifies a modifiled file
 

#### git fetch [remote-name]

"git fetch" command pulls the data to your local repository,
it doesn't automatically merge it with any of your work or
modify what you're currently working on;
you have to merge it manually into your work when you're ready;  
instead you can use "git pull" command


#### git push [remote-name] [branch-name]

this command pushes the data to the server


#### tags

Git uses two main types of tags: lightweight and annotated;
- a lightweight tag is very much like a branch that doesn't change -
  it's just a pointer to a specific commit;  
- annotated tags are store as full objects in the Git database

it is generally recommended to create annotated tags

```git
$ git tag
```
will show all tags;

```git
$ git show v1.5
```
will show the tag v1.5;

```git
$ git tag --annotate v1.5 --message 'Message for a tag'
```
Will create an annoated tag;

```git
$ git tag v1.5-lw
```
will create a lightweight tag;

```git
$ git tag --annotate v1.2 9fceb02
```
will create an annotated tag v1.2 for the commit "9fceb02";

```git
$ git push origin v1.5
```
will push the v1.5 tag to the server (origin in this case);

```git
git push origin --tags
```
will push all tags to the server (origin in this case);