---
title: Trust Architecture
parent: 4. gittuf for Maintainers
layout: default
nav_order: 2
permalink: /documentation/maintainers/design/
---

## Trust Architecture

gittuf's metadata is based on (but not a copy of) [The Update Framework] (TUF).

{: .info}

> Even if you have experience with TUF, we suggest you still read through to
> understand how gittuf manages trust.

In many Git security systems today, compromising a single user with elevated
privilege leads to a total compromise of the repository at that user's level. If
the user has the highest level of privilege (e.g. an administrator), this may
lead to catastrophic consequences for the repository.

To combat this, gittuf uses two features from TUF that serve as a check on any
single user's power: **thresholding** and **delegations**.

### Thresholding

Git security systems often require that _only one_ user of a certain privilege
level approve an action (e.g. modify branch protection rules). While this is
convenient as the user need not seek the approval of anyone else to perform an
action, this means that this user becomes a **single point of failure**.

If the user turns malicious (e.g. disgruntled employee, or other reasons), they
will be able to perform their actions until their powers are revoked by another
user. If the user's credentials are compromised by a malicious actor, then the
outcome is the same, compromise until credential revocation.

To combat this, gittuf allows for users' power to be split up across a set of
multiple users. To perform a privileged action, multiple users must agree (by
signing metadata) to the action before it is considered valid. This threshold
can be any arbitrary number up to the number of users with a certain privilege.

### Delegations

Users' powers are often implicit, i.e. a repository owner will be inherently be
able to perform actions of any lower privilege. As discussed above, compromise
of a user means they are able to do anything that their privilege level allows
them to do.

gittuf implements **delegations**, which _distribute power_ across multiple
trust levels. For example, consider a repository owner that has the power to
both appoint other repository owners, and set rules for how regular users should
be able to commit to the repository.

In gittuf, the repository owner has the ability to appoint other repository
owners, but **NOT** the ability to to set rules for regular users. In order to
be able to set rules for regular users, the owner _must explicitly designate
themselves as having that ability_.

This opt-in mechanism means that a privileged user cannot perform an action
they are not explicitly allowed to without leaving a trace in the repository's
policy history.

Now, let's look at the various levels of trust gittuf defines.

## Trust Levels

gittuf defines three basic levels of trust, in decreasing order of privilege:

1. Root of Trust
2. Policy Administrator
3. Delegated Policy Administrator
4. Contributors

Each level carries different abilities and responsibilities.

### Root of Trust

Trust in gittuf is not an infinite chain, and it must be stop somewhere with a
set of users who are **ultimately trusted**, i.e. repository owners. These users
sign the root of trust metadata, which details at least:

1. The set of users that comprise the root of trust
2. The threshold of users required to update the root of trust metadata
3. The set of policy administrators

To learn more about the operations these users can perform, see [Root of Trust].

### Policy Administrator

Appointed by the root of trust, these users are responsible for defining the
write access controls for the _entire_ repository. These users may define rules
that grant certain repository users write access to certain branches or files in
the repository. Administrators may also delegate a part of the Git namespace
(e.g. certain branches or files) to be managed by another administrator.

To learn more about the operations these users can perform, see [Policy].

### Delegated Policy Administrator

These administrators are appointed by other policy administrators, and can only
set gittuf policy for the part of the repository they are authorized to do so.
Should these administrators wish, they may delegate all or part of their
abilities to another administrator (and further along).

### Contributors

Contributors are all other users in the repository, who may or may not have
write access to the repository (e.g. an actual contributor or a random user on
the internet). Contributors in the repository have no ability to set gittuf
policy, and can only make changes as dictated by the gittuf policy.

These users may read gittuf policy to understand where they are allowed to make
changes in the repository. These users can perform the operations detailed in
[Using gittuf].

## Next: Root of Trust

Now, let's dive into how to set up the root of trust in gittuf in [Root of
Trust].

[The Update Framework]: https://theupdateframework.io
[Root of Trust]: /documentation/maintainers/root
[Policy]: /documentation/maintainers/policy
[Using gittuf]: /documentation/using
