---
title: Verifying with gittuf
parent: 3. Using gittuf
layout: default
nav_order: 2
permalink: /documentation/using/verifying
---

# Verifying with gittuf

Verification is perhaps the most important operation in gittuf. After all, none
of what we've gone over elsewhere in this documentation matters much if gittuf
can't tell you your repository was compromised.

{: .warning}

> gittuf **does NOT** verify changes made _before_ it was initialized and a
> policy applied. This means any activity that occurred before gittuf was
> applied is accepted as-is. Of course, an attacker cannot easily rewrite
> history, but if you had a commit before gittuf was applied that would violate
> your gittuf policy now, gittuf will not catch it.

Because of this, invoking verification in gittuf is made to be as simple as
possible. In fact, it's just one command that you will need to use most of the
time: `gittuf verify-ref`.

## Verifying a Reference

gittuf verifies changes per branch. So, if you have two branches that have
gittuf policies applied to them, you will need to run the verification workflow
twice, once for each branch. To run verification, invoke the `gittuf verify-ref`
command:

```
gittuf verify-ref <branch name>
```

gittuf will verify that all changes on the branch are valid, starting from the
first where a policy was defined, to the most recent commit. If nothing is
printed to the console, then verification was successful.

{: .info}

> If you're interested in how gittuf verifies changes, or need to see what
> commit is problematic, run the command with the `--verbose` flag. Be aware
> that there may be **a lot** of output to sift through!


## Next: Users Without gittuf

After reading the documentation so far, you might be wondering how users who
don't use gittuf can work on a repository that uses gittuf. Let's see how that
works in [Users without gittuf].

[Users without gittuf]: /documentation/using/no-gittuf
