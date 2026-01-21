---
title: Initialization
parent: Root of Trust
layout: default
nav_order: 1
permalink: /documentation/maintainers/root/initialization
has_toc: no
---

# Initialization

The **very first** operation you will need to perform with gittuf is
initializing the root of trust. **No other operation can take place until this
is done.**

To initialize the root of trust, ensure you are in the directory of your
repository, and use `gittuf trust init`:

```
gittuf trust init -k <your signing key>
```

This will create the `refs/gittuf/policy-staging` reference, with a singular
commit that contains the initialized gittuf root metadata.

## Next: Managing Root of Trust Users and Administrators

Next, let's take a look at how to add (or remove) other root of trust users
and policy administrators in [Managing Users].

[Managing Users]: /documentation/maintainers/root/users
