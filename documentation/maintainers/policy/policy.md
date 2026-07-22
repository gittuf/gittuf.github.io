---
title: Policy
parent: 4. gittuf for Maintainers
layout: default
nav_order: 3
permalink: /documentation/maintainers/policy
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
done using **delegated rule files**. These rule files behave similarly to the
primary rule file, with the exception that they must be manually specified in
policy operations.

## Next: Managing Principals

Let's start by defining the users that policy rules will refer to, in
[Managing Principals].

[Managing Principals]: /documentation/maintainers/policy/users
[Policy Administrator]: /documentation/maintainers/design#policy-administrator
[Delegated Policy Administrator]: /documentation/maintainers/design#delegated-policy-administrator
[defining users]: /documentation/maintainers/policy/users
