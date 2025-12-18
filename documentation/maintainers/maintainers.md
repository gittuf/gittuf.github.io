---
title: 4. gittuf for Maintainers
parent: Documentation
layout: default
nav_order: 4
permalink: /documentation/maintainers
---

# Part 4: gittuf for Maintainers

gittuf is capable of enforcing write access control policies on Git
repositories, without the need for a centralized platform to enforce said
policies. Because of this, you must use the gittuf tool to define your desired
policy for your Git repository, similar to how you use Git.

As with any security policy, designing an effective policy can be challenging
task. This guide is intended to help you understand how gittuf works, so that
you can build and apply your policy.

## A Note on Signing Keys

gittuf uses cryptographic signatures to bind data (e.g. commits, code approvals,
etc...) to specific people. Because of this, users need to be signing commits so
that gittuf can identify that the user making a commit is authorized to do so.
gittuf currently is able to verify commits signed with GPG, SSH, and [Sigstore]
keys.

The setup guide for both [Maintainers] and [Contributors] details how to
configure Git so that commits are signed properly.

{: .heads-up}

> gittuf currently does not support GPG keys for _signing gittuf metadata_. This
> means that contributors in your repository are OK if they use GPG keys to sign
> commits, but any time gittuf policy is updated, you must use an SSH or
> Sigstore key. See [#904] on GitHub.


## Reading this Guide

The administration documentation for gittuf is divided into five parts, with
each section taking you through how each part of gittuf metadata is initialized
and managed.

While you need not read it in order if you are only interested in a specific
part, we suggest reading through [Trust Architecture] first so you understand
how gittuf structures trust and user permissions, as well as definitions used in
this section.

## Next: Trust Architecture

Let's take a quick look at how gittuf handles trust in [Trust Architecture].

[Sigstore]: https://sigstore.dev
[Maintainers]: /quickstart/maintainer
[Contributors]: /quickstart/contributor
[#904]: https://github.com/gittuf/gittuf/issues/904
[Trust Architecture]: /documentation/maintainers/design
