---
title: Users Without gittuf
parent: 3. gittuf for Contributors
layout: default
nav_order: 4
permalink: /documentation/contributors/no-gittuf
---

# Users Without gittuf

Because gittuf is backwards compatible with Git, users who do not use gittuf can
still access and work on the repository that gittuf protects. While this works
without any problem for users who simply read the repository's contents, anyone
who needs to contribute code will not generate the proper gittuf metadata.
Thankfully, any user running gittuf and trusted to write at least somewhere in
the repository can perform the needed steps.

## Workflow

A user without gittuf may sign commits if they wish. gittuf can use these signatures
to ascertain that the commits did in fact come from the user they claim to. The
user's signing key(s) must be added to gittuf policy for this process to work.

If the user does not sign commits, a maintainer may step in and record the changes
in the RSL in lieu of the contributor signing their commits. Note that recording
the changes in the RSL is required either way.

{: .heads-up}

> Make sure to verify the changes that you are recording, as gittuf will treat
> your recording these changes as an approval by you!

After the non-gittuf user has pushed their changes to the remote repository, one
gittuf user must pull the changes down, and run the RSL record workflow:

```
gittuf rsl record <branch name>
```

The workflow must be invoked for every branch that the user made changes to.
After that, invoking gittuf's synchronization workflow manually will push the
needed metadata up to the server:

```
gittuf sync
```

## Next: Approving Changes

For the final chapter in this section, we take a look at how you can approve
changes using gittuf to meet a threshold of greater than one in [Approving
Changes].

[Approving Changes]: /documentation/contributors/approving-changes
