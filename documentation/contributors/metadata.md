---
title: gittuf Metadata
parent: 3. gittuf for Contributors
layout: default
nav_order: 1
permalink: /documentation/contributors/metadata
---

# gittuf Metadata

gittuf's design allows users to verify that the repository's security policy was
followed, without needing to rely on a centralized hosting platform. Because of
this, gittuf must store metadata in the Git repository itself. This is done
natively, and allows for backwards compatibility with users and services that
use Git.

Git, however, does not automatically generate or synchronize the metadata gittuf
needs in order to verify changes to the repository. To that end, you can
manually invoke gittuf to perform the necessary actions.

While we won't dive into extreme detail on how gittuf is designed, let's first
take a look at the metadata that underpins gittuf.

{: .info}

> If you're interested in learning more about gittuf's design, see the [gittuf
> design document].

## Git References

To store gittuf metadata in Git repositories, gittuf uses **custom namespaces**,
which can be thought of as "hidden branches". These references are just like the
branches you work with in Git, but they are separate and share no history with
the branches you normally use.

These references contain commits, each of which contains some state of gittuf
metadata. gittuf uses the following references:

```
refs/gittuf/reference-state-log # Tracks the Reference State Log (RSL)

refs/gittuf/policy-staging # Tracks gittuf policy that has not yet been applied
refs/gittuf/policy # Tracks gittuf policy

refs/gittuf/attestations # Tracks the attestations used by gittuf
```

Let's look at each part of metadata.

## Reference State Log (RSL)

Determining the order of commits on a single branch is easy, but determining the
order of commits across multiple branches is more difficult. This is one of the
several reasons why gittuf includes a dedicated log, which we call the RSL.

With the RSL, every time a gittuf policy operation takes place (e.g. someone is
granted or revoked permissions), and at least every time a user pushes commits
they have created on a branch, an entry is recorded. This (among many other
desirable properties) allows us to determine an ordering of events that occur.

For example, let's say Alice works at Company A. As part of her work, she is
authorized to make changes to the `main` branch of a repository. She later
leaves for a different company, and has her permissions removed. The commits she
created while at Company A should still be considered valid, but she should not
have the ability to create new commits after her departure. The RSL allows us to
determine which commits Alice creates should be validated against a certain
policy.

## gittuf Policy

gittuf policy is represented on-disk as JavaScript Object Notation (JSON). The
policy is stored as several Git blobs, which are collected in commits. Each
commit on the gittuf `refs/gittuf/policy` reference represents a state of gittuf
policy.

For example, Alice being added to the policy, Bob being added to the policy, and
Carol being added to the policy would be three separate policy states, and
therefore commits.

To allow administrators to make changes to the policy that need to be applied
all at once, gittuf also has the `refs/gittuf/policy-staging` reference, which
contains the _proposed_ gittuf policy, but is not yet enforced.

## Attestations

Git commits can only carry one signature. gittuf supports rules which require
more than one person to approve changes introduced by commits. To achieve this,
gittuf uses **attestations**.

An attestation is simply a signed claim, e.g. "I approve these changes being
merged into the `main` branch." These claims are then signed by the user making
said claim, and added to `refs/gittuf/attestations`.

Attestations in gittuf extend beyond this, with the gittuf GitHub App (detailed
in Part 6), and other uses of attestations throughout gittuf.

## Next: Automatic Metadata Management

Now, let's see how gittuf can automatically handle updates to its metadata
in the background of your daily workflow with [Automatic Metadata Management].

[gittuf design document]: https://github.com/gittuf/gittuf/blob/main/docs/design-document.md
[Automatic Metadata Management]: /documentation/contributors/automatic
