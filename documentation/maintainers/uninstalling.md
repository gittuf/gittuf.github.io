---
title: Resetting/Uninstalling gittuf
parent: 4. gittuf for Maintainers
layout: default
nav_order: 7
permalink: /documentation/maintainers/uninstalling
---

# Resetting/Uninstalling gittuf

Should you wish to start over with gittuf or stop using it, reinitializing
gittuf metadata or removing gittuf entirely is simple.

Before you do so, we ask that you [submit an issue] describing any issues you're
facing, so that we can help you and fix the issue if needed.

## Resetting gittuf

{: .warning }

> Any users which have already pulled down gittuf metadata for the repository
> must also follow this procedure. **This is by design**, to prevent silent
> takeovers of the repository.

To reset gittuf's metadata, you must delete the references which store gittuf
metadata:

```
git update-ref -d refs/gittuf/reference-state-log
git update-ref -d refs/gittuf/policy-staging
git update-ref -d refs/gittuf/policy
git update-ref -d refs/gittuf/attestations
```

After this, [reinitialize gittuf's root of trust].

## Uninstalling gittuf

Removing the gittuf binary from your system depends on how you installed it.

### Winget

```
winget remove gittuf.gittuf
winget remove gittuf.git-remote-gittuf
```

### Homebrew

```
brew remove gittuf
```

### Linux

If you installed gittuf via a package manager, use that package manager's
uninstallation command, e.g. `apt remove gittuf`. Otherwise, if you downloaded
the gittuf binaries directly, you need only delete them.

### FreeBSD

Deleting the downloaded gittuf binaries will uninstall gittuf.

### Source

gittuf's compiled binaries are stored inside your `$GOHOME`. On Linux/Unix
platforms, this tends to be `$HOME/go/bin`, with the `gittuf` and
`git-remote-gittuf` binaries inside.

[submit an issue]: https://github.com/gittuf/gittuf/issues/new
[reinitialize gittuf's root of trust]: /documentation/maintainers/root/initialization
