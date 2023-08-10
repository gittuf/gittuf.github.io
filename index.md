---
title: Home
layout: home
nav_order: 1
---

gittuf provides a security layer for Git using the concepts introduced by
[The Update Framework (TUF)]. Among other features, gittuf handles key 
management for all developers on the repository, allows you to set
permissions for repository branches, tags, files, etc., lets you use
new cryptographic algorithms (SHA256, etc.), protects against a 
[large array of attacks] which Git is vulnerable to, and more --- all
while being backwards compatible with Github, GitLab, Gerrit, etc.

## Current Status

gittuf is currently in an early-development stage and is therefore considered
pre-alpha. Please do not use it in a production system or repository.


[The Update Framework (TUF)]: https://theupdateframework.io
[large array of attacks]: https://ssl.engineering.nyu.edu/papers/torres_toto_usenixsec-2016.pdf
