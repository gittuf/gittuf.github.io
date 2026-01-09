---
title: Contributor Quickstart
parent: Installation and Quickstart
layout: default
nav_order: 2
permalink: /quickstart/contributor
---

# Contributor Quickstart

Now that gittuf is installed, you need to set your repository to use gittuf to
help synchronize gittuf-specific metadata, and ensure that you are signing
commits.

## Using `gittuf::`

If you haven't cloned the repository you need to work on yet, simply add the
`gittuf::` prefix to the URL where your Git repository is located. For example,

```
git clone gittuf::git@github.com:owner/repo
```

If you have cloned the repository you need to work on, navigate to it, and then
update the remote server URL from which you fetch changes from. For example,
if your default server is `origin` (in most cases), run:

```
git remote set-url origin gittuf::git@github.com:owner/repo
```

## Verifying Changes

gittuf handles operations automatically in the background, but if you prefer
to check manually at any time, simply run:

```
gittuf verify-ref <branch name>
```

## Next Steps

That's all there is to using gittuf on a daily basis. Unless you prefer to poke
around, gittuf should stay out of your way. If it doesn't, please [open an
issue] on our issue tracker so we can investigate.

If you're a more hands-on user interested in poking around with gittuf, see
the [gittuf Documentation].

[open an issue]: https://github.com/gittuf/gittuf/issues/new
[gittuf Documentation]: /documentation
