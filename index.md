---
title: Home
layout: home
nav_order: 1
---

![gittuf logo](https://raw.githubusercontent.com/gittuf/community/bd8b367fa91fab0fddaa1943e0131e90e04e6b10/artwork/PNG/gittuf_horizontal-color.png)

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

## Installation & Get Started

See the [get started guide] in the [gittuf repository].

[The Update Framework (TUF)]: https://theupdateframework.io
[other attacks]: https://ssl.engineering.nyu.edu/papers/torres_toto_usenixsec-2016.pdf
[Open Source Security Foundation (OpenSSF)]: https://openssf.org/
[Supply Chain Integrity Working Group]: https://github.com/ossf/wg-supply-chain-integrity
[gittuf repository]: https://github.com/gittuf/gittuf
[get started guide]: https://github.com/gittuf/gittuf/blob/main/docs/get-started.md
