---
title: Switch Git Submodule from HTTPS to SSH
layout: post
date: 2024-06-12
description: I don't know who use HTTPS for git submodule and I hate to enter username password
tags: etc
---

I was assigned to review code in the project and found that the team use Git Submodule with HTTPS, which is require them to enter username and password every time they want to install the project.

It might be good for them, I guess. But, it's not good for me. I'm a lazy bastard and I hate to remember password.

So, we should switch Git Submodule from HTTPS to SSH

The current Git Submodule

```shell
cat .gitmodules # Why we call it "Git submodule", when the config is "Gitmodues"? 
[submodule "common"]
  path = common
  urk = https://githost/project-repo.git
```

This file tells that we can pull source code from `https://githost/project-repo.git` into path `common/` with this command 

```shell
git submodule update
```

But I won't do that because the url is HTTPS, which require me to login with username and password. I don't want to do that since I've SSH key.

So, I just have to change the url into SSH

```dot
[submodule "common"]
  path = common
  urk = ../project-repo.git
```

Then run

```shell
git submodule sync 
git submodule update

# clone submodule into common/
```

Now Git submodule will clone with your current access or in my case clone without asking for username and password.
