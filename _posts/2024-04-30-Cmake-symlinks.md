---
title: Cmake and Symbolic Links
author: suranap
date: 2024-04-30 11:00:00
categories: [HPC]
tags: [tips]
---

On HPC machines you are given a paltry 40-50GB of HOME directory storage. As result you have to juggle your files around to stay below the [quota](https://docs.nersc.gov/filesystems/#summary). HPC machines generally offer some kind of [scratch space](https://docs.nersc.gov/filesystems/perlmutter-scratch/) with much more space, but there are usually caveats like no backups and files expire after some time if not used. 

I build multiple versions of my projects using cmake in different build subdirectories. To manage my space I use symbolic links to put them onto the scratch space. The default cmake version on Frontier is (as of this post's date) 3.23.2. Unfortunately cmake fails with strange error messages that says it doesn't have a rule to build "../src/your/files". Cmake fixed this [issue](https://gitlab.kitware.com/cmake/cmake/-/issues/21819) in 3.24.0 with this [commit](https://gitlab.kitware.com/cmake/cmake/-/commit/d33b12d84b59fd3310c31de7d9c3f83b28b681e2). So make sure you use a version of cmake > 3.23 to use symbolic links for your build directories. 
