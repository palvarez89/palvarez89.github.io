---
layout: post
title: Playing with git submodules
date: 2016-04-07 12:27:10.000000000 +01:00
tags:
- DNS
- dominios
status: publish
type: post
published: true
meta:
  _edit_last: '1'
author:
  login: palvarez89
  email: palvarez89@gmail.com
  display_name: palvarez89
  first_name: 'Pedro'
  last_name: 'Alvarez Piedehierro'
---


In a project I'm currently working on, we have decided to create a repository
with thousands of git submodules. The main goal for such a monstrosity is to
be able to synchronise thousands of components without having a huge monolithic
repository.

An example of what I'm talking about is [this repostory](https://github.com/ssssam/baserock-minimal-system-submodules-example)
which contains 74 submodules. These submodules are repositories needed to
build a minimal Linux system with [Baserock].

So, now imagine that you are working with a checked out version of this repository,
and you want to checkout a different branch, or just update the current branch
you are in to get latest changes in the remote (`git pull`)... Does that just
work when you have also submodules checked out? The answer is *"No"*.

I started researching and I identified 4 possible situations that can
happen when you change to a different commit in the parent repository:

* A submodule has been created
* A submodule has changed its url
* A submodule has changed its version
* A submodule has been removed

<!--more-->

[Baserock]: http://wiki.baserock.org/
