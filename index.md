---
title: Home
layout: home
nav_order: 1
---

![gittuf logo](https://raw.githubusercontent.com/gittuf/community/bd8b367fa91fab0fddaa1943e0131e90e04e6b10/artwork/PNG/gittuf_horizontal-color.png)

gittuf provides a security layer for Git using some concepts introduced by [The
Update Framework (TUF)]. Among other features, gittuf handles key management for
all developers on the repository, allows you to set permissions for repository
branches, tags, files, etc., protects against [other attacks] Git is vulnerable
to, and more --- all while being backwards compatible with GitHub, GitLab, etc.

gittuf is a sandbox project at the [Open Source Security Foundation (OpenSSF)]
as part of the [Supply Chain Integrity Working Group].

## Current Status

gittuf is currently in alpha. It is not yet intended for use in a production
system or repository. We're now actively working on making gittuf more usable so
it has lesser impact on developer workflows. Contributions are welcome, please
refer to the [contributing guide]. Some of the features listed above are being
actively developed, please refer to the [roadmap] and the repository's issue
tracker for more details.

## Installation & Get Started

See the [get started guide] in the [gittuf repository].

[The Update Framework (TUF)]: https://theupdateframework.io
[other attacks]: https://ssl.engineering.nyu.edu/papers/torres_toto_usenixsec-2016.pdf
[Open Source Security Foundation (OpenSSF)]: https://openssf.org/
[Supply Chain Integrity Working Group]: https://github.com/ossf/wg-supply-chain-integrity
[gittuf repository]: https://github.com/gittuf/gittuf
[get started guide]: https://github.com/gittuf/gittuf/blob/main/docs/get-started.md
[roadmap]: https://github.com/gittuf/gittuf/blob/main/docs/roadmap.md
[contributing guide]: https://github.com/gittuf/gittuf/blob/main/CONTRIBUTING.md
