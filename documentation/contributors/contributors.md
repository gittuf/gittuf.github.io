---
title: 3. gittuf for Contributors
parent: Documentation
layout: default
nav_order: 3
permalink: /documentation/contributors
has_toc: no
---

# Part 3: gittuf for Contributors

gittuf's design allows users to verify that the repository's security policy was
followed, without needing to rely on a centralized hosting platform. Because of
this, gittuf must store metadata in the Git repository itself.

Without getting into too much detail, gittuf needs to record each push (and its
contents) that you make to the remote Git repository that you (and other users)
make.

gittuf supports two operating modes for recording your pushes and verifying
others' changes:

- gittuf can automatically record pushes and verify the repository, or,
- You can manually record your pushes and verify the repository

Depending on how you wish to use gittuf and the sensitivity of the repository
that you are working on, you might want to choose a different option than others
(even other users working on the same repository as you).

For most users, we recommend letting gittuf automatically record pushes and
verify in the background, unless you:

- Would like to manually invoke gittuf synchronization and verification
  operations.
- Are debugging an issue.

{: .info}

> We won't dive into detail in this section about how gittuf is designed, but if
> you're interested in learning more about gittuf's design, see the [gittuf
> design document].

## Next: Signing Keys

Let's first take a look at an important prerequisite for using gittuf, [Signing
Keys].

[RSL Entries]: /documentation/contributors/metadata
[gittuf design document]: https://github.com/gittuf/gittuf/blob/main/docs/design-document.md
[Signing Keys]: /documentation/contributors/signing-keys