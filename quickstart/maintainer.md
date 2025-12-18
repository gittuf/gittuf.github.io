---
title: Maintainer Quickstart
parent: Installation and Quickstart
layout: default
nav_order: 3
permalink: /quickstart/maintainer
---

# Maintainer Quickstart

gittuf contains a setup wizard that will get you started with a basic security
policy that you can build on as needed.

## Configuration

{: .experimental}

> The `gittuf setup` features is not yet merged, and requires the code from
> [#1124](https://github.com/gittuf/gittuf/pull/1124) to be merged.

Run the setup wizard to configure a basic gittuf policy:

```
gittuf setup
```

## Daily Workflow

If you plan to push your repository to a service such as GitHub, gittuf can
automatically handle recording and verifying commits. Simply add the `gittuf::`
prefix to your repository's remote URL, e.g. `git@github.com:owner/repo` becomes
`gittuf::git@github.com:owner/repo`.

You can update your Git configuration with this change as follows:
```
git remote set-url origin gittuf::git@github.com:owner/repo
```

## Verifying Changes

To verify that the gittuf policy was followed on the repository, run:

```
gittuf verify-ref <branch name>
```

## Next Steps

If you'd like to learn more about how gittuf works or adjust gittuf's security
policy to better fit your needs, see the [gittuf Documentation].

[Sigstore]: https://sigstore.dev
[gittuf Documentation]: /documentation
