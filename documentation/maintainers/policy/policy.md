---
title: Policy
parent: 4. gittuf for Maintainers
layout: default
nav_order: 3
permalink: /documentation/maintainers/policy
has_toc: no
---

# Policy

Once the root of trust has been initialized properly, it is time to define the
security policy for the repository.

{: .heads-up}

> You must be either a [Policy Administrator], or a [Delegated Policy
> Administrator] in order to manage the gittuf policy. The root of trust users
> appoint these administrators.
>
> Root of Trust users (by default) are **not** Policy Administrators, nor are
> Contributors.

## Policy Files

gittuf contains two types of policy files: **primary rule files** and
**delegated rule files**.

### The Primary Rule File

By default, gittuf places all rules defined in the **primary rule file**. This
rule file is used by default for all gittuf policy operations, unless otherwise
specified. In most cases, your repository will only need this rule file.

### Delegated Rule Files

If you wish to delegate your policymaking authority to another user, this is
done using **delegated rule files**. We will take a look at these later. For
more information, see [Delegated Policies].

## Policy Initialization

As with the root of trust, the policy must be initialized before it can be
modified.

To initialize the primary rule file, ensure you are in the directory of your
repository, and use `gittuf policy init`:

```
gittuf policy init -k <your signing key>
```

This will create the primary rule file.

## Defining Users and Creating Rules

With the policy created, let's see how we can define users and create rules,
starting with [defining users].

[Policy Administrator]: /documentation/maintainers/design#policy-administrator
[Delegated Policy Administrator]: /documentation/maintainers/designs#delegated-policy-administrator
[Delegated Policies]: /documentation/maintainers/policy/rules#delegated-policies
[defining users]: /documentation/maintainers/policy/users
