---
layout: post
title: Playing with git submodules
date: 2016-04-07 12:27:10.000000000 +01:00
tags:
- Git
- submodules
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

An example of what I'm talking about is [this repostory] which contains
74 submodules. These submodules are repositories needed to build a minimal
Linux system with [Baserock].

[this repostory]: https://github.com/ssssam/baserock-minimal-system-submodules-example
[Baserock]: http://wiki.baserock.org/

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


It's really important that we can automate all these possible situations because,
as I said before, we are going to deal with thousands of them, and doing things
manually is not the right thing.


### A submodule has been created

When the checked out version includes a new submodule that wasn't present in
the previous version, you will have to initiate it and checkout the contents.
This is basically the same situation that you have when you first clone
a repository without using `--recursive`

To do this:

    git submodule init
    git submodule update


### A submodule has changed its version

When you check out a version that has changed the version of any of the
submodules you will see something like this when running `git diff`:

    $ git diff
    diff --git a/usbhid-dump b/usbhid-dump
    index b18e816..81eab80 160000
    --- a/usbhid-dump
    +++ b/usbhid-dump
    @@ -1 +1 @@
    -Subproject commit b18e816cbf65fe3b7f53d1d275f550c0c18e9b0f
    +Subproject commit 81eab80f40fd6c0d7ffb3734e27480ea5617807a


In this case, instead of removing the submodule and doing starting again,
you can just run the following command to update the contents of it.

    git submodules update


### A submodule has changed its url

Sometimes, some repositories move to  different git servers, or even to different
places within the same git server. This is something that happens, and as
a consequence, some repositories that are using one these moving repositories
as a submodule, will need to update their urls to point to the new place.

How to handle this situation with your checked out version of the repository?
First of all you will need to make sure that we use the new url, and then we can
update the submodule itself.

To achieve this you have to:

    git submodule sync
    git submodule update


### A submodule has been removed

This also can happen... If this is the case, the submodule will appear in
`git status` as an untracked directory.

Normally in this case, you might not care about the untracked files, but
in my case, I will want to have a clean checkout of the repository with its
submodules.

To clean them you will have to run:

    git clean -xdff

Note that the double 'ff' is intentional, otherwise it won't remove the
submodule from your current tree (See `man git-clean` for more information).
Also note that this command will remove any untracked file from your tree.


## Conclusion

After investigating theses cases, I can say that it will be possible to use
multiple git submodules, and that is not going to be a nightmare to work with
them.

The best approach to move to a different version in the parent repository
and updating the submodules in one go will be:

    git submodule init     # Initialize possible new repositories
    git submodule sync     # Update possible changes in urls
    git submodule update   # Update submodules to the right version
    git clean -xdff        # Remove possible removed repositories

Note that I haven't considered cases of various levels of submodules, but
I think this is enough for today :)
