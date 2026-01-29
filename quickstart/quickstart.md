---
title: Installation and Quickstart
layout: default
nav_order: 2
has_toc: false
permalink: /quickstart/
---

# Installation and Quickstart

Welcome! This guide will get you up and running with gittuf.

## Install gittuf

First, you need to install gittuf. Run the appropriate commands for your OS, or
[install from source] if you prefer.

### Windows

Install gittuf from Winget:

```
winget install gittuf.gittuf
winget install gittuf.git-remote-gittuf
```

### macOS

[Install Homebrew] if you haven't already, and then install gittuf from
Homebrew:

```
brew install gittuf
```

### Linux

gittuf is bundled with various package managers, but is often out of date. We
recommend installing gittuf with Go itself. [Install Go], and run the following
commands:

```
go install github.com/gittuf/gittuf@latest
go install github.com/gittuf/gittuf/internal/git-remote-gittuf@latest
```

### FreeBSD

gittuf is not (yet) packaged with `pkg` on FreeBSD systems. Download the
binaries for the [latest gittuf release], and add them to your `$PATH`. Make
sure to download both `gittuf` and `git-remote-gittuf`.

## Using gittuf

{: .experimental}

> The `gittuf setup` utility is currently experimental, and is pending inclusion
> in gittuf with PR [#1124]. In the meantime, we suggest using the [legacy
> getting started guide].

Next, change your working directory to the Git repository you want to use gittuf
with. If you have not cloned or initialized the repository yet (i.e. `git
init`), do this now.

Additionally, if you will be making commits or managing gittuf, ensure that you
have a [signing key set up in your Git configuration].

Now, run the setup utility:

```
gittuf setup
```

The setup utility will guide you through using gittuf on the repository.

## Next Steps

Unless you prefer to poke around, gittuf should stay out of your way. If it
doesn't, please [open an issue] on our issue tracker so we can investigate. If
you're a maintainer or a more hands-on user interested in poking around with
gittuf, see the [gittuf Documentation].

[install from source]: https://
[Install Homebrew]: https://brew.sh/
[Install Go]: https://go.dev/doc/install
[latest gittuf release]: https://github.com/gittuf/gittuf/releases/latest
[Sigstore]: https://sigstore.dev
[signing key set up in your Git configuration]: /documentation/contributors/signing-keys
[open an issue]: https://github.com/gittuf/gittuf/issues/new
[gittuf Documentation]: /documentation
[#1124]: https://github.com/gittuf/gittuf/pull/1124
[legacy getting started guide]: https://github.com/gittuf/gittuf/blob/main/docs/get-started.md#create-keys
