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

## How do you want to use gittuf?

The instructions from here on out are different depending on how you need to use
gittuf. If you're a user that:

- wants to verify a repository against its own gittuf policy, you're a
  **consumer**.
- is contributing changes to a Git repository with gittuf enabled, you're a
  **contributor**.
- is setting up or managing gittuf on a Git repository, you're a **maintainer**.

To continue, please select how you're using gittuf:

[I'm a Consumer](/quickstart/consumer){: .btn .btn-green }
[I'm a Contributor or Maintainer](/quickstart/contributor-maintainer){: .btn .btn-purple }

[install from source]: https://
[Install Homebrew]: https://brew.sh/
[Install Go]: https://go.dev/doc/install
[latest gittuf release]: https://github.com/gittuf/gittuf/releases/latest
[Sigstore]: https://sigstore.dev
