---
title: Quickstart
layout: default
nav_order: 2
has_toc: false
permalink: /quickstart/
---

# Quickstart

Welcome! This guide will get you up and running with gittuf.

## Install gittuf

First, you need to install gittuf. Run the appropriate commands for your OS.

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
recommend installing gittuf from source. [Install Go], and run the following
commands:

```
git clone https://github.com/gittuf/gittuf
cd gittuf
make
```

## User Type

The instructions from here on out are different if you're a **administrator**
that is setting up gittuf on a Git repository, or if you're a **contributor**
working on a repository that uses gittuf.

Please select how you're using gittuf:

[I'm a Contributor](/quickstart/contributor){: .btn .btn-green }
[I'm an Administrator](/quickstart/admin){: .btn .btn-blue }

[Install Homebrew]: https://brew.sh/
[Install Go]: https://go.dev/doc/install
