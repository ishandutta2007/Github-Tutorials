Recommended Git and GitHub Tools
===

Git Command Line Enhancements
---

### [diff-so-fancy](https://github.com/so-fancy/diff-so-fancy)

![diff so fancy screenshot](../img/git-diff-screenshot.png)

### [git-extras](https://github.com/tj/git-extras)

**Ubuntu**

```
$ sudo apt-get install git-extras
```

**Mac OS X with Homebrew**

```
$ brew install git-extras
```

```
$ git-summary


 project  : github-roam
 repo age : 2 years, 7 months
 active   : 40 days
 commits  : 124
 files    : 101
 authors  :
    72   Fengda HUANG  58.1%
    29   Fengda Huang  23.4%
     8   Phodal HUANG  6.5%
     3   Phodal Huang  2.4%
     2   yangpei3720   1.6%
     2   WangXiaolong  1.6%
     2   TZS           1.6%
     1   安正超        0.8%
     1   Li            0.8%
     1   Qiuer         0.8%
     1   SCaffrey      0.8%
     1   oncealong     0.8%
     1   zminds        0.8%
```

Intellij IDEA
---

Since my daily development tool is the enterprise version of Intellij IDEA, I've become somewhat reliant on it. The most commonly used feature is: **when fixing bugs, tracing changes to files**. Understanding why a line of code was changed, who made the change, etc.

Intellij IDEA

Git, GitHub Desktop Enhancements
---

### SourceTree

SourceTree is convenient for looking at projects not written by me, to find some issues within them. The reason is: **IntelliJ IDEA takes a lot of time to index when first opening a project**. Unfortunately, the current SourceTree clients require an Atlassian account login.

Gitflow branch merging, viewing

![SourceTree screenshot](../img/sourcetree.jpg)

### GitHub Desktop

![GitHub Desktop](../img/github-desktop.jpg)

Git Entertainment
---

### githug

```
$ githug

********************************************************************************
*                                    Githug                                    *
********************************************************************************
No githug directory found, do you wish to create one? [yn]  y
Welcome to Githug!

Name: init
Level: 1
Difficulty: *

A new directory, `git_hug`, has been created; initialize an empty repository in it.
```


```
$ githug play

********************************************************************************
*                                    Githug                                    *
********************************************************************************
Congratulations, you have solved the level!

Name: config
Level: 2
Difficulty: *

Set up your git name and email, this is important so that your commits can be identified.
```

```
#1: init
#2: config
#3: add
#4: commit
#5: clone
#6: clone_to_folder
#7: ignore
#8: include
#9: status
#10: number_of_files_committed
#11: rm
#12: rm_cached
#13: stash
#14: rename
#15: restructure
#16: log
#17: tag
#...
```

### Gource

![Gource history](../img/gource.jpg)