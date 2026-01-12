---
title: Initialization
parent: Policy
layout: default
nav_order: 1
permalink: /documentation/maintainers/policy/initalization
has_toc: no
---

# Policy Initialization

As with the root of trust, the policy must be initialized before it can be
modified.

## Primary Rule File

To initialize the primary rule file, ensure you are in the directory of your
repository, and use `gittuf policy init`:

```
gittuf policy init -k <your signing key>
```

This will create the primary rule file.

## Delegated Rule File

If you have been authorized to manage a part of the security policy for the
repository by way of a delegation, you must initialize your rule file before you
can apply rules.

To initialize a delegated rule file, ensure you are in the directory of your
repository, and use `gittuf policy init`, specifying the file name to create.

```
gittuf policy init -k <your signing key> --policy-name <policy file name>
```

{: .info}

> Ensure that the file name you specify matches the policy rule name granting
> you delegated policy powers.
>
> For example, if the rule granting you delegated policy powers is named
> `protect-feature`, then you must create and operate within a policy file named
> `protect-feature`.

This will create the delegated rule file.

## Next: Defining Users and Creating Rules

With the policy created, let's see how we can define users and create rules,
starting with defining users in [Managing Principals].

[Managing Principals]: /documentation/maintainers/policy/users
