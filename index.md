---
title: Home
layout: home
nav_order: 1
---

![gittuf logo](https://raw.githubusercontent.com/gittuf/community/bd8b367fa91fab0fddaa1943e0131e90e04e6b10/artwork/PNG/gittuf_horizontal-color.png)

gittuf is a platform-agnostic Git security system. The maintainers of a Git
repository can use gittuf to protect the contents of a Git repository from
unauthorized or malicious changes. Most significantly, gittuf's policy controls
and enforcement is not tied to your source control platform (SCP) or "forge",
meaning any developer can independently verify that a repository's changes
followed the expected security policies. In other words, gittuf removes the
forge as a single point of trust in the software supply chain!

gittuf is an incubating project at the [Open Source Security Foundation
(OpenSSF)] as part of the [Supply Chain Integrity Working Group].

## Features

Some of gittuf's features are:
- **Key distribution, rotation, and revocation:** While Git supports
  cryptographically signing commits and tags, it does not provide mechanisms to
  securely manage these keys. To verify a signature, you must identify the
  trusted keys using out-of-band mechanisms. In the case of a compromise and a
  subsequent key revocation, you must also identify which historic signatures
  issued [before the revocation can still be
  trusted](https://karl.kornel.us/2017/10/welp-there-go-my-git-signatures/).
  gittuf implements key management features to securely distribute, rotate, and
  revoke keys trusted for a repository.
- **Granular write access control rules:** gittuf rules grant granular
  permissions to protect portions of the repository like specific branches,
  tags, and files/folders from unauthorized changes. Each rule can also be
  configured to specify the minimum number of approvals required to satisfy the
  rule.
- **Self-contained, {system}-agnostic:** gittuf associates all aspects of a
  repository's security such as policies and activity information with the
  repository itself. While this is primarily to avoid trusting any other system
  for the security of a repository, it also means that important information
  such as the history of code review approvals are tracked in the repository
  itself, meaning this information is not lost when a repository is moved from
  one platform to another!
- **Backwards compatible:** gittuf is designed to be compatible with existing
  systems in the Git ecosystem, including popular SCPs like GitHub and GitLab.
  gittuf can also be used with existing repositories.

## Current Status

gittuf is currently in beta. gittuf's metadata is versioned, and updates should
not require reinitializing a repository's gittuf policy. We recommend trying out
gittuf in addition to existing repository security mechanisms you may already be
using (e.g., forge security policies). We're now actively working on making
gittuf more usable so it has lesser impact on developer workflows. Contributions
are welcome, please refer to the [contributing guide]. Some of the features
listed above are being actively developed, please refer to the [roadmap] and the
repository's issue tracker for more details.

## Installation & Get Started

See the [get started guide] in the [gittuf repository].

## Note for Academic Researchers

gittuf is developed by a combination of academic and industry security
researchers, and has been [peer-reviewed]. To cite gittuf, use:

```bibtex
{% raw %}
@inproceedings{yelgundhalli2025,
    author = {Aditya Sirish A Yelgundhalli and Patrick Zielinski and Reza Curtmola and Justin Cappos},
    title = {{Rethinking Trust in Forge-Based Git Security}},
    booktitle = {{32nd Network and Distributed System Security Symposium (NDSS 2025)}},
    year = {2025},
    isbn = {979-8-9894372-8-3},
    address = {San Diego, CA},
    url = {https://www.ndss-symposium.org/ndss-paper/rethinking-trust-in-forge-based-git-security/},
    publisher = {{Internet Society}},
}
{% endraw %}
```

[Open Source Security Foundation (OpenSSF)]: https://openssf.org/
[Supply Chain Integrity Working Group]: https://github.com/ossf/wg-supply-chain-integrity
[gittuf repository]: https://github.com/gittuf/gittuf
[get started guide]: https://github.com/gittuf/gittuf/blob/main/docs/get-started.md
[roadmap]: https://github.com/gittuf/gittuf/blob/main/docs/roadmap.md
[contributing guide]: https://github.com/gittuf/gittuf/blob/main/CONTRIBUTING.md
[peer-reviewed]: https://www.ndss-symposium.org/wp-content/uploads/2025-1008-paper.pdf
