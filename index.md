---
title: Home
layout: home
nav_order: 1
---

gittuf provides a security layer for Git using some concepts introduced by [The
Update Framework (TUF)]. Among other features, gittuf handles key management for
all developers on the repository, allows you to set permissions for repository
branches, tags, files, etc., lets you use new cryptographic algorithms (SHA256,
etc.), protects against [other attacks] Git is vulnerable to, and more --- all
while being backwards compatible with GitHub, GitLab, etc.

gittuf is a sandbox project at the [Open Source Security Foundation (OpenSSF)]
as part of the [Supply Chain Integrity Working Group].

## Current Status

gittuf is currently in alpha. Please do not use it in a production system or
repository.

## Installation

The [gittuf repository] provides pre-built binaries that are signed and
published using [GoReleaser]. The signature for these binaries are generated
using [Sigstore], using the release workflow's identity. Please use release
v0.1.0 or higher, as prior releases were created to test the release workflow.
Alternatively, gittuf can also be installed using `go install`.

To build from source, clone the repository and run `make`. This will also run
the test suite prior to installing gittuf. Note that Go 1.21 or higher is
necessary to build gittuf.

```bash
$ git clone https://github.com/gittuf/gittuf
$ cd gittuf
$ make
```

[The Update Framework (TUF)]: https://theupdateframework.io
[other attacks]: https://ssl.engineering.nyu.edu/papers/torres_toto_usenixsec-2016.pdf
[Open Source Security Foundation (OpenSSF)]: https://openssf.org/
[Supply Chain Integrity Working Group]: https://github.com/ossf/wg-supply-chain-integrity
[gittuf repository]: https://github.com/gittuf/gittuf
[GoReleaser]: https://goreleaser.com/
[Sigstore]: https://www.sigstore.dev/
