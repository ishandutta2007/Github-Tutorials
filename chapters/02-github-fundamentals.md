# Basic Git Knowledge and Using GitHub

## Git

From the perspective of a typical developer, Git offers the following functionalities:

1. Clone a repository (including code and version history) from a server to your local machine.
2. Create branches on your own machine and modify code.
3. Commit code on the branches you created locally.
4. Merge branches on your local machine.
5. Create a new branch, fetch the latest version of the code from the server, and merge it with your main branch.
6. Generate a patch and send it to the maintainer.
7. Wait for the maintainer's feedback. If the maintainer detects a conflict between two developers (a conflict they can resolve themselves), they will ask them to resolve the conflict first before one of them submits the patch. If the maintainer can resolve it themselves, or if there is no conflict, the patch is accepted.
8. Methods for developers to resolve conflicts among themselves: developers can use the `pull` command to resolve conflicts. After resolving the conflicts, they then submit the patch to the maintainer.

From the perspective of a main developer (assuming the main developer doesn't write code themselves), Git offers the following functionalities:

1. Check emails or use other means to review the submission status of developers.
2. Apply patches, resolve conflicts (can be done by themselves, or they can ask developers to resolve and resubmit. For open source projects, they also need to decide which patches are useful and which are not).
3. Submit the results to the public server and notify all developers.

### Getting Started with Git

If you are using Git for the first time, you need to set your name and email:

```
$ git config --global user.name "Your Name"
$ git config --global user.email "your.email@example.com"
```

Cloning a repository to your local machine essentially copies the code to your computer and places it under Git's management:

```
$ git clone git@github.com:someone/symfony-docs-chs.git
```

You can now modify the code you've copied locally (the symfony-docs-chs project contains documents in rst format). When you feel you've completed a certain amount of work and want to make a staged commit:

Add all current changes in the directory to this local repository:

```
$ git add .
```

Or add only a specific file:

```
$ git add -p
```

We can run

```
$ git status
```

to see the current state. The image below shows the state before adding:

![Before add](../img/before-add.png)

The following image shows the state after adding:

![After add](../img/after-add.png)

You can see the state change from yellow to green, i.e., from 'unstaged' to 'added'.

## GitHub

Wikipedia describes it as:

> GitHub is a shared virtual hosting service for storing software code and content projects using Git version control. It was developed by GitHub, Inc. (formerly Logical Awesome) developers Chris Wanstrath, PJ Hyett, and Tom Preston-Werner, written in Ruby on Rails.

Let's also look at the official introduction:

> GitHub is the best place to share code with friends, co-workers, classmates, and complete strangers. Over eight million people use GitHub to build amazing things together.

What else can it be used for?

- A website
- A free blog
- Managing profiles
- Collecting materials
- A resume
- Managing code snippets
- Hosting a programming environment
- Writing

And so on. It seems like a feast, but what else do you need to know?

### Version Management and Software Deployment

When jQuery[^jQuery] released version `2.1.3`, it had 152 commits. We can see commit messages like:

 - Ajax: Always use script injection in globalEval … bbdfbb4
 - Effects: Reintroduce use of requestAnimationFrame … 72119e0
 - Effects: Improve raf logic … 708764f
 - Build: Move test to appropriate module fbdbb6f
 - Build: Update commitplease dev dependency
 - ...

### GitHub and Git

> Git is a distributed version control system originally written by Linus Torvalds for managing Linux kernel development. After its launch, Git achieved great success in other projects, especially within the Ruby community. Currently, many well-known projects including Rubinius, Merb, and Bitcoin use Git. Git can also be used by deployment tools like Capistrano and Vlad the Deployer.

> GitHub can host various Git repositories and provides a web interface. However, unlike other services such as SourceForge or Google Code, GitHub's unique selling point is the ease of forking from another project. Contributing code to a project is very simple: first, click the "fork" button on the project site, check out the code, add your modifications to the forked repository, and finally request a code merge from the project maintainer via the built-in "pull request" mechanism. Some have already called GitHub the MySpace for coders.

### Creating a Project on GitHub

Next, let's try creating a project on it:

![GitHub Roam](../img/github-roam-create.jpg)

You'll then see the following prompt:

![GitHub Roam](../img/project-init.jpg)

It provides multiple ways to create a project:

> …or create a new repository on the command line

```
echo "# github-roam" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:phodal/github-roam.git
git push -u origin master
```

> …or push an existing repository from the command line

```
git remote add origin git@github.com:phodal/github-roam.git
git push -u origin master
```

If you've completed the steps above, then I think you'd want to know what kind of project you need.

## Analysis of Popular GitHub Projects

I've analyzed some GitHub user behaviors before. Now, let's talk about 'Stars' on GitHub. (As of March 9, 2015, 23:00.)

User | Project Name | Language | Star | Url
-----|------------- |----------|------|----
twbs | Bootstrap | CSS | 78490 | [https://github.com/twbs/bootstrap](https://github.com/twbs/bootstrap)
vhf | free-programming books | - | 37240 | [https://github.com/vhf/free-programming-books](https://github.com/vhf/free-programming-books)
angular | angular.js | JavaScript | 36,061 | [https://github.com/angular/angular.js](https://github.com/angular/angular.js)
mbostock | d3 | JavaScript | 35,257 | [https://github.com/mbostock/d3](https://github.com/mbostock/d3)
joyent | node | JavaScript | 35,077 | [https://github.com/joyent/node](https://github.com/joyent/node)

The list above shows the top 5. Looking at the distribution of projects with more than 10,000 Stars, there are 82 in total:

Language | Project Count
---------|-------------
JavaScript | 37
Ruby | 6
CSS | 6
Python | 4
HTML | 3
C++ | 3
VimL | 2
Shell | 2
Go | 2
C | 2

Type Distribution:

 - Libraries and Frameworks: e.g., `jQuery`
 - Systems: e.g., `Linux`, `hhvm`, `docker`
 - Configuration Sets: e.g., `dotfiles`
 - Auxiliary Tools: e.g., `oh-my-zsh`
 - Tools: e.g., `Homebrew` and `Bower`
 - Resource Collections: e.g., `free programming books`, `You-Dont-Know-JS`, `Font-Awesome`
 - Others: Resumes, e.g., `Resume`

## Pull Request

Besides creating projects, we can also create Pull Requests (PRs) to contribute.

### My First PR

My first PR was for a small Node.js CoAP-related library. The reason was simple: its README.md was incorrect, which prevented me from proceeding.

```diff
 const dgram       = require('dgram')
-    , coapPacket  = require('coap-packet')
+    , package     = require('coap-packet')
```

A simple yet useful change. Another example is:

```diff
 else
   cat << END
 $0: error: module ngx_pagespeed requires the pagespeed optimization library.
-Look in obj/autoconf.err for more details.
+Look in objs/autoconf.err for more details.
 END
   exit 1
 fi
```

### CLA

CLA stands for Contributor License Agreement. When submitting Pull Requests to some large organizations or institutions, you may need to sign this agreement. They will ask you in your Pull Request, and they will only accept your PR after you go to their website to register and agree to the terms.

Below is a PR I submitted for Google:

![Google CLA](../img/google-cla.png)

And one for Eclipse:

![Eclipse CLA](../img/eclipse-cla.png)

Both required me to sign a CLA.
