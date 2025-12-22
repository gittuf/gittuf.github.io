---
title: 3. Using gittuf
parent: Documentation
layout: default
nav_order: 3
permalink: /documentation/using
has_toc: no
---

# Part 3: Using gittuf

gittuf can be configured in one of two ways:

- Automatically handle gittuf operations, or,
- Require the user to manually to sync gittuf data and verify the repository

Depending on how you wish to use gittuf and the sensitivity of the repository
that you are working on, you might want to choose a different option than others
(even other users working on the same repository as you). For most users, we
recommend letting gittuf automatically manage its operations in the background,
unless you:

- Are an administrator who must manage the security policy gittuf applies.
- Would like to manually invoke gittuf synchronization and verification
  operations.
- Are debugging an issue.

## Automatic Management

gittuf ships with a program (`git-remote-gittuf`) known as a _Git transport_,
which is used by your computer to talk with Git servers (e.g. GitHub, GitLab,
Bitbucket, etc...). Because of this, it must be invoked every time you run
commands such as `git pull` or `git push`, and serves as a reliable place to run
common gittuf tasks. The transport automatically does the following for you:

- Create [RSL Entries] as needed
- Synchronize gittuf metadata
- Verify that the repository is compliant with gittuf policy

This means that (in most cases), you need not interact with gittuf to do the
work you already do on your Git repository. There is one exception, [Approving
Changes] with multiple users required.

If you are a root of trust user or administrator, you can use the gittuf
transport, but will still need to interact with gittuf manually to set policies.
See [Part 4: Administering gittuf] for more information.


## Manual Management

Manually using gittuf involves two primary processes for both contributors and
administrators:

- Managing gittuf Metadata
- Verifying with gittuf

## Next: gittuf Metadata

Let's start with managing [gittuf Metadata].

[RSL Entries]: /documentation/using/metadata
[gittuf Metadata]: /documentation/using/metadata
[Approving Changes]: /documentation/using/approving-changes
[Part 4: Administering gittuf]: /documentation/administrators
