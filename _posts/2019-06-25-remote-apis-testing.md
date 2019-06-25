---
layout: post
title: Remote APIs testing
date: 2019-06-25 17:07:10.000000000 +01:00
toc: true
tags:
- Bazel
- Buildbarn
- Buildfarm
- BuildGrid
- Gitlab CI
- Remote Execution
status: publish
type: post
published: true
meta:
  _edit_last: '1'
author:
  login: palvarez89
  email: pedro@alvarezpiedehierro.com
  display_name: palvarez89
  first_name: 'Pedro'
  last_name: 'Alvarez Piedehierro'
---

A couple of months ago, I was tasked with drafting a system that would continously test the compability of Bazel with different remote execution services.

Originally it looked like:


I couldn't be more wrong:

- Building latest builbarn, conatiner using bazel? Using sed for the right tag.
- Latest bazel needs latest toolchain
  - not possible to point to latest
- Latest toolchain needed latest Ubuntu container
- Not all the software can do the hacks we do.

Conclusions
- too many moving parts, all syncronised


