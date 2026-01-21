---
title: Installation from Source
parent: Installation and Quickstart
layout: default
nav_order: 3
permalink: /quickstart/source
---

# Installation from Source

As gittuf is free- and open-source software, you may compile it yourself.

## Prerequisites

gittuf is written in [Go], so you need to [install Go] in order to compile the
gittuf source code. We suggest installing Go from the official website, as it
provides the latest version of Go, and gittuf tends to require the latest
Go version to compile.

After you install Go, ensure that `GOBIN` (the directory where compiled Go
binaries are installed) is in your `PATH`.

## Acquiring gittuf Source Code

The official gittuf source code is on GitHub, and can be cloned using `git
clone`:

```
git clone git@github.com:gittuf/gittuf
cd gittuf
```

## Building gittuf

We recommend running `make`, which will run all tests and then build gittuf:

```
make
```

These tests can take several minutes depending on your operating system and
hardware. To skip these tests and just build gittuf, run:

```
make just-install
```

gittuf will be installed to your `$GOBIN`, which is often `$HOME/go/bin` on
Linux/Unix platforms.

## Verifying the gittuf Repository with gittuf

We use gittuf to secure the gittuf repository itself, and you can verify that
your copy of the gittuf repository was not tampered with.

Once you have installed gittuf, use gittuf to retrieve gittuf's metadata:

```
gittuf sync
```

Then, run gittuf verification inside the gittuf repository:

```
gittuf verify-ref main
```

This will check that all activity on the main branch adheres to gittuf policy.
gittuf will by default only print anything to the screen if there is an error
verifying the repository.

## Next: Quickstart

Now, return to the [quickstart instructions] to set up your signing keys and
gittuf.

[Go]: https://go.dev
[install Go]: https://go.dev/doc/install
[quickstart instructions]: /quickstart#how-do-you-want-to-use-gittuf
