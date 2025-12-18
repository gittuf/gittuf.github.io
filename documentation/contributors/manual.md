---
title: Manual Metadata Management
parent: 3. gittuf for Contributors
layout: default
nav_order: 3
permalink: /documentation/contributors/manual
has_toc: no
---

# Manual Metadata Management

If you prefer to manually manage gittuf's metadata, you need to make a few
changes to your current Git workflow.

First, every time you either:

- push your commits/changes to the remote server, or,
- make a commit/change on your local copy of the Git repository,

you need to inform gittuf about the changes that you made. To do so, for each
branch that you made changes to, you run:

```
gittuf rsl record <branch name>
```

gittuf uses your signing key to sign the entry, and then adds it to the RSL.

After you have made all desired changes to your repository and are ready to push
your changes to the remote server, you need to also ensure that gittuf's
metadata is also along for the ride. To that end, you may use gittuf, by
running:

```
gittuf sync
```

Or, you may use Git itself to synchronize gittuf's references:

```
git push <remote> refs/gittuf/*
git fetch <remote> refs/gittuf/*:refs/gittuf/*
```

{: .heads-up}

> Don't forget to manually run gittuf verification as well! See [Verifying with
> gittuf] to see how to do this.

## Next: Users Without gittuf

After reading the documentation so far, you might be wondering how users who
don't use gittuf can work on a repository that uses gittuf. Let's see how that
works in [Users without gittuf].

[Verifying with gittuf]: /documentation/consumers/verifying
[Users without gittuf]: /documentation/contributors/no-gittuf
