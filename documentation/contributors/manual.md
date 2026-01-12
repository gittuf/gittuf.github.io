---
title: Manual Push Recording
parent: 3. gittuf for Contributors
layout: default
nav_order: 3
permalink: /documentation/contributors/manual
has_toc: no
---

# Manual Push Recording

If you prefer to manually record your pushes and verify the repository, you need
to make a few changes to your current Git workflow.

First, every time you push your commits/changes to the remote server, you need
to inform gittuf about the changes that you made. To do so, for each branch that
you made changes to, you run:

```
gittuf rsl record <branch name>
```

gittuf uses your signing key to sign the entry, and then records this entry in
the repository.

{: .info}

> You may, if you prefer, invoke `gittuf rsl record` every time that you make a
> commit/change on your local copy of the Git repository, instead of when you
> push your changes. This does not impact the security that gittuf provides, so
> as long as you run the `record` command **right before** you push your changes
> (i.e. to ensure that all changes are recorded).

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

{: .warning}

> **Don't forget to manually run gittuf verification as well!** See [Verifying
> with gittuf] to see how to do this.

## Next: Users Without gittuf

After reading the documentation so far, you might be wondering how users who
don't use gittuf can work on a repository that uses gittuf. Let's see how that
works in [Users without gittuf].

[Verifying with gittuf]: /documentation/consumers/verifying
[Users without gittuf]: /documentation/contributors/no-gittuf
