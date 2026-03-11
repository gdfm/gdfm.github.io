---
layout: post
title: "git to svn patch"
date: 2011-05-24
categories: ["Technology"]
tags: ["git", "GSoC", "patch", "pig", "svn"]
author: "melmeric"
permalink: /2011/05/24/git-to-svn-patch/
---

After discovering **git** I practically fell in love with it.
So I decided to use the [git Apache mirror](http://git.apache.org/) for [Pig](//git.apache.org/pig.git) for this year's GSoC.
One problem i found is that the ASF (Apache Software Foundation) uses svn (subversion) patches, but git by default produces a slightly different diff format that is not readily understood by the *patch* utility. A simple workaround for this issue is to use the *--no-prefix* option of *git diff*. (it should also work to use -p1 instead of -p0 in the patch command).
To make completely transparent that I am using a different repository, I also keep a separate *pristine* tree checked out of svn and always up to date with trunk. To try my modifications, I can simply check out the branch I want to try out, generate a patch, apply it on the fly on the pristine svn tree and run *ant test* while I continue working on the git tree. To generate the final patch to submit I resort again to svn.

```

git co PIG-XXXX
git diff trunk --no-prefix | patch -p0 -d ../pigpristine/
cd ../pigpristine/ && svn diff > PIG-XXXX.patch

```

In the snippet I assume the git and svn tree are siblings in the filesystem, and that the svn tree is called *pigpristine*.