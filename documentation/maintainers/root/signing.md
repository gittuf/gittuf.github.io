---
title: Signing the Root Metadata
parent: Root of Trust
layout: default
nav_order: 4
permalink: /documentation/maintainers/root/signing
---

# Signing (and Applying) the Root Metadata

Once you have added the desired users to the root of trust and appointed the
policy administrators, the root of trust must be signed and made active.

This process varies depending on whether other root of trust users must sign
your changes.

## I'm the Only Root of Trust User / Threshold of One

If you are the only root of trust user, or the root (not policy) threshold is
set to one, then the process is easy.

First, _stage_ the changes with `gittuf trust stage`. If your default remote is
`origin` (as is in most cases), run:

```
gittuf trust stage origin
```

This will automatically push your changes to the remote. If you do not wish to
do so, append `--local-only`:

```
gittuf trust stage --local-only
```

Next, _apply_ the changes with `gittuf trust apply`. `apply` uses the same
`--local-only` semantics as `stage`:

```
gittuf trust apply origin
```

gittuf will make your changes to the root of trust active and enforceable. These
changes will be reflected in `refs/gittuf/policy`.

## Multiple Users Must Approve Changes / Threshold > 1

If other root of trust users must sign your changes before they are valid, the
process is a bit more involved.

First, _stage_ the changes with `gittuf trust stage`. If your default remote is
`origin` (as is in most cases), run:

```
gittuf trust stage origin
```

gittuf will push the changes to the remote. Now, other users must pull the
changes to their computers to sign them.

The other users must tell gittuf to pull down the changes made to the root of
trust metadata:

```
gittuf sync
```

Now, the other users must each sign the changes with `gittuf trust sign`:

```
gittuf trust sign -k <the user's signing key>
```

Finally, each user must sync their changes after signing with `gittuf sync`.

When all users have signed off on the changes to the root of trust, you can
finish the process and make the changes live with:

```
gittuf trust apply origin
```

gittuf will make your changes to the root of trust active and enforceable. These
changes will be reflected in `refs/gittuf/policy`.

## Next: Rule Files

In the next section, we take a look at how we can 