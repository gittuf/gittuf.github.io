---
title: Features and Goals
layout: default
nav_order: 2
---

gittuf implements a subset of the TUF specification with some modifications to
make it a better fit for Git repositories. A more detailed description of gittuf
can be found in the living [design document].

**Note:** Some of the features listed here are still under active development.
Contributions are welcome!

## Table of Contents
{: .no_toc }

1. TOC
{:toc}

## Features

gittuf has the following key features.

### Root of Trust

gittuf uses TUF semantics to establish a root of trust for a Git repository. The
owners of the Git repository are expected to maintain this root of trust, which
is fundamental to the rest of gittuf's features.

### Key Distribution and Revocation

gittuf allows repository owners to declare and distribute the public keys
required to verify Git commit and tag signatures. While Git provides mechanisms
for signing with GPG, SSH keys, and X.509 certificates, discovering verification
materials and identifying whether they can be trusted is left to users.

Unfortunately, this has some shortcomings. For one, it is not trivial to always
identify the right public keys to use. Additionally, using existing distribution
and revocation systems like the PGP/GPG Web of Trust has unfortunate side
effects. If a key is revoked, it is unclear which of its _historic_ signatures
can continue to be trusted. gittuf tackles these issues by directly associating
public keys with the repository and by continuously tracking policies so that it
is unambiguous when a key is revoked.

### Permissions

gittuf builds on the improved key distribution and revocation mechanisms by
leveraging Git's commit and tag signing to define access control policies.
Repository owners can define rules such as the set of developers authorized to
make changes to a branch or create a tag. In addition, repository owners can
also create policies that dictate which users can make changes to specific files
in the repository. In each of these cases, developers are primarily identified
by their signing keys. gittuf provides a granular permission model that can be
used to create branch protection rules, maintain write-permissions in monorepos,
and more, all without reliance on a centralized security system!

## Goals

While developing gittuf, we have the following goals.

### Unopinionated / Agnostic

gittuf provides features to implement different policies without **requiring**
the use of specific systems or tools. For example, gittuf supports a variety of
signing mechanisms such as GPG keys and [Sigstore]'s [gitsign].

### Compatible

gittuf is designed with great care to be compatible with standard Git
repositories. All additional artifacts are stored in Git's object store in a
gittuf-specific namespace. These artifacts are not visible in the "main"
contents of a repository, and therefore do not create any clutter.


[design document]: https://github.com/gittuf/gittuf/blob/main/docs/design-document.md
[Sigstore]: https://sigstore.dev
[gitsign]: https://github.com/sigstore/gitsign
