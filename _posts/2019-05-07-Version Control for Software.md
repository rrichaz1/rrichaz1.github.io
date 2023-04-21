Version control at its most basic can be compared to authors releasing versions of their books. Similarly programmers release incremental versions of their code.

In the earliest days’ programmers would keep copies of the code by filing them by date etc. This was a manual process and error prone. If the person failed to file properly the changes would be lost. The systems would crash and programs had features of auto save that the users could use to recover. We see the examples of those in Microsoft word, excel. The first software project I worked was on IBM AS/400. IBM systems are closed systems so the operating system and the programs all reside on one machine. The source code would be set up in libraries and only one person could work on one program/piece of code at a time. It had pretty robust auto recovery feature. 
The biggest mishap I had done was once I while trying out a command I deleted a whole library that lost 1 month’s work of effort by a whole team. Thanks to the tape backups and some friendship with operators who had access to the tape backups, we restored everything back and all was safe and sound. 
Soon after at a client site, I got acquainted with ALDON the version control system on AS/400. It seemed a little tedious but after the previous mishap I was sold on the concept. 

Later as I started working on Java, we had multiple people working on MVC architecture. It was important to use Version control systems. At that time CVS (Concurrent Versions System) was the system of choice. CVS uses a client–server architecture: a server stores the current version(s) of a project and its history, and clients connect to the server in order to "check out" a complete copy of the project, work on this copy and then later "check in" their changes. Teams spread across geographies worked on the trunk as maintaining branches was very tedious. People in one location would check in the changes and go home when the team in another location would come in to work. Inevitably some people would check in partial changes and then part of the day would go in somehow making the code compile and run. Around six years back we migrated to git. The migration process brought its own nightmares but we soon got comfortable with it. It is a paradigm shift as GIT is a distributed version system, where each user keeps a clone of the repository. It makes branching very easy.

Now we have teams working on different branches. Once the branch is tested and certified then it is merged to trunk avoiding all the heartaches. In the beginning, version control looks like an overhead but over time we realize its importance. It can be used to trace back the changes and if programmers use proper merge messages, it can even answer some of the whys. Why a programmer made a change and what was the thought process behind selecting an option, is a challenge in long running project. Literate programming tries to solve this problem by weaving the why with the actual code. Just like any tool or methodology, its proper usage can be very beneficial. 
  





“Git was initially developed to meet the demands of a control version system to manage the source code of the Linux operating system kernel. The development of Linux by its very nature required a distributed versioning model, where commits are scattered in several parallel lines of development (branches) and must go through an approval process. This need led to the development of Git by the leader of the Linux project, Linus Torvalds. After the release of the first version in 2005 Git was handled to its current maintainer: Junio Hamano, a software engineer at Google.”

git remote -v
git remote add upstream <branch>
git fetch upstream
git branch
git checkout master
git merge upstream/master

[https://eclipsesource.com/blogs/2011/06/09/git-lessons-learned/](https://eclipsesource.com/blogs/2011/06/09/git-lessons-learned/)
[https://nvie.com/posts/a-successful-git-branching-model/](https://nvie.com/posts/a-successful-git-branching-model/)
[https://stackoverflow.com/questions/20984802/how-can-i-keep-my-fork-in-sync-without-adding-a-separate-remote/21131381#21131381](
https://stackoverflow.com/questions/20984802/how-can-i-keep-my-fork-in-sync-without-adding-a-separate-remote/21131381#21131381)
[https://help.github.com/en/articles/fork-a-repo](https://help.github.com/en/articles/fork-a-repo)
[https://help.github.com/en/articles/syncing-a-fork](https://help.github.com/en/articles/syncing-a-fork)
