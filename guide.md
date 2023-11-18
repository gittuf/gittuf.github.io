---
title: User Guide
layout: default
nav_order: 4
---

Many of gittuf's core features are under active development and, therefore, are
rapidly changing. A more detailed user guide will be published here when gittuf
reaches beta. For now, this guide presents the workflow for using gittuf's alpha
releases.

## Prerequisites

Before using gittuf, we suggest having a valid signing key specified in your
Git configuration (i.e. `git config --local user.signingkey`). See the
[Git manual](https://git-scm.com/book/en/v2/Git-Tools-Signing-Your-Work)
as well as [gitsign](https://gitsign.dev) for more information. Note that
having a valid signing key is required for any gittuf operations that write
changes to the repository.

## Root of Trust

First, it is necessary to establish the
[root of trust](https://github.com/gittuf/gittuf/blob/main/docs/design-document.md#managing-gittuf-root-of-trust)
for the gittuf policies. To do so, the repository's owners must use the `trust`
subcommand. The root of trust can be initialized using `gittuf trust init`,
presenting the command with the root key.

After the root of trust itself is established, it must be updated to declare the
primary policy's keys. This is achieved using `gittuf trust add-policy-key`. A
companion `gittuf trust remove-policy-key` may be used to revoke a previously
trusted key for the primary policy.

## gittuf Policies

[The policies](https://github.com/gittuf/gittuf/blob/main/docs/design-document.md#managing-gittuf-policies)
themselves are managed using the `gittuf policy` subcommand. If a policy file
does not already exist, it must be first initialized using `gittuf policy init`.

After a policy file is established, it may be updated with specific rules,
setting constraints on one or more namespaces. Specifically, `gittuf policy
add-rule` can be used to add a rule to the specified policy file, while its
companion `gittuf policy remove-rule` can be used to remove a previously
declared constraint. Policies can protect files (by specifying `file:` in the
rule pattern, such as `file:README.md`) as well as Git refs (such as
`git:refs/heads/main`).

## Reference State Log

gittuf implements an authenticated
[reference state log](https://github.com/gittuf/gittuf/blob/main/docs/design-document.md#reference-state-log-rsl)
that tracks changes to the different Git references (eg. branches, tags) in a
repository. Currently, when a change is made to some reference, it must be
recorded in the RSL using `gittuf rsl record`. An RSL annotation entry can be
created using `gittuf rsl annotate`. Note that manually recording changes in
the RSL is not required when you update the policy, as the RSL records changes
to the policy namespace automatically.

## Verification

gittuf supports various types of verification workflows. First, gittuf allows
users to verify policy conformance for a Git reference. This can be invoked
using `gittuf verify-ref`. In addition, gittuf also provides equivalents to
Git's `verify-commit` and `verify-tag`. These gittuf equivalents use the trusted
keys in gittuf policies to verify commit and tag signatures. Here are some
examples on how to verify:

- `gittuf verify-ref -f main` will verify the `main` branch.

- `gittuf verify-commit HEAD` will verify the commit at `HEAD`.

## Syncing gittuf Namespaces

Currently, gittuf's custom namespaces must be synced separately. The RSL may be
synced using `gittuf rsl remote` which includes support for push and pull
operations. Similarly, the `gittuf trust remote` or `gittuf policy remote`
commands can be used to sync the policy namespace.
