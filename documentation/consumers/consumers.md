---
title: 2. gittuf for Consumers
parent: Documentation
layout: default
nav_order: 2
permalink: /documentation/consumers
has_toc: no
---

# Part 2: gittuf for Consumers

Verifying a repository against its security policy is a complicated task to do
correctly. For the everyday software consumer, gittuf is designed to make this
simple.

{: .heads-up}

> gittuf follows [Git's order for resolving reference names]. This means that if
> you have ambiguous reference names, such as the tag `main` and the branch
> `main`, gittuf will perform operations on the **tag**, not the branch!
>
> We suggest you use fully-qualified reference names to avoid ambiguity and
> ensure that you are operating on the correct reference. In our example above,
> the fully-qualified reference name of the tag `main` would be
> `refs/tags/main`, while the branch would be `refs/heads/main`.

## Next: Verification

Let's take a look at [how verification works].

[Git's order for resolving reference names]: https://git-scm.com/docs/gitrevisions#_specifying_revisions
[how verification works]: /documentation/consumers/verifying
