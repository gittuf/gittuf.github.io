---
title: Verifying with gittuf
parent: 2. gittuf for Consumers
layout: default
nav_order: 1
permalink: /documentation/consumers/verifying
---

# Verifying with gittuf

Verification is perhaps the most important operation in gittuf. After all, none
of what we've gone over elsewhere in this documentation matters much if gittuf
can't tell you your repository was compromised.

In gittuf, verifying the repository is done per reference, which can be a branch
or tag.

{: .warning}

> gittuf **does NOT** verify changes made _before_ it was initialized and a
> policy applied. This means any activity that occurred before gittuf was
> applied is accepted as-is. Of course, an attacker cannot easily rewrite
> history, but if you had a commit before gittuf was applied that would violate
> your gittuf policy now, gittuf will not catch it.

## Verifying a Branch

Identify the branch that you would like to verify changes to. Then, to run
verification, invoke the `gittuf verify-ref` command:

```
gittuf verify-ref <branch name>
```

{: .heads-up}

> If you want to verify multiple branches, you will need to run the verification
> workflow for each branch.

gittuf will verify that all changes on the branch are valid, starting from the
first where a policy was defined, to the most recent commit. If nothing is
printed to the console, then verification was successful.

{: .info}

> If you're interested in how gittuf verifies changes, or need to see what
> commit is problematic, run the command with the `--verbose` flag. Be aware
> that there may be **a lot** of output to sift through!

## Verifying a Tag

Identify the tag that you would like to verify. Then, just as with branches,
invoke the `gittuf verify-ref` command:

```
gittuf verify-ref <tag name>
```

{: .heads-up}

> If you want to verify multiple tags, you will need to run the verification
> workflow for each tag.

## Performance Optimization

{: .experimental}

gittuf currently uses the Git binary for operations, which incurs a performance
penalty due to process spawning overhead. Starting with `v0.17.0`, gittuf ships
with an experimental `go-git` backend that significantly improves performance.

Since it is still in testing, you must manually opt in to using this backend,
which can be done by setting the environment variables `GITTUF_DEV=1` and
`GITTUF_STORER=go-git`.

We encourage you to use this backend and report any issues to us on GitHub.

## Next: gittuf and SLSA

Next, let's look at an experimental feature: [gittuf support for SLSA]. 


[official GitHub repository for gittuf]: https://github.com/gittuf/gittuf
[gittuf support for SLSA]: /documentation/consumers/slsa
