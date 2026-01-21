---
title: Root of Trust
parent: 4. gittuf for Maintainers
layout: default
nav_order: 2
permalink: /documentation/maintainers/root
---

# Root of Trust

The root of trust is the set of users ultimately trusted in gittuf. In addition
to encoding the users that compose the root of trust, the root metadata contains
information on the repository, as well as [global rules](#global-rules).

## Configuration

In most cases, the root of trust is a part of gittuf metadata that is largely
"set it and forget it". You only need to modify the root of trust metadata when
you are changing:

- the users that make up the root of trust
- the policy administrators
- repository information (e.g. canonical location, etc...)
- global rules

{: .warning}

> It is imperative that the root of trust users **safeguard and DO NOT lose**
> their signing keys. If there are insufficient root of trust users to make
> changes (e.g. the threshold is three but only two users have access to their
> keys), then it will be **impossible** to recover gittuf metadata, and you will
> need to [reset gittuf].

## Next: Initializing the Root of Trust

Let's start by initializating gittuf's root of trust in [Initialization].

[global rules]: /documentation/maintainers/root/global-rules
[reset gittuf]: /documentation/maintainers/uninstalling#resetting-gittuf
[Initialization]: /documentation/maintainers/root/initialization
