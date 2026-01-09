---
title: Managing Principals
parent: Policy
layout: default
nav_order: 1
permalink: /documentation/maintainers/policy/users
---

# Managing Principals

Earlier on, we saw how we defined the root of trust users and policy
administrators by using their signing keys. With gittuf policy, we have a richer
method for accommodating users that may use multiple signing keys.

In gittuf policy, users added to the policy are instead called **principals**.
Principal entries in gittuf contain the following information:

- The principal's identifier
- The principal's signing keys, which can be a mix of GPG, SSH, or [Sigstore] keys
- Custom metadata to be used by Policy Administrators as needed

Currently, the following principal types are supported:

- **Person**, which is just a singular human/bot.
- **Key**, a legacy principal that is just a singular key. You may see this in
  old versions of gittuf metadata.

When verifying changes made to the repository, gittuf identifies principals by
their signing keys. Before you can create rules in gittuf policy, you must first
define users to use in the policy's rules.

{: .info}

> Note that defined users are specific to policy files, which means that if you
> are a Delegated Policy Administrator, you must define any users you need in
> your policy, irrespective of whether they were defined in other policy files.
>
> In addition, you must also use the `--policy-name` flag to specify the policy
> to add the user to, otherwise they will be added to the primary policy.

## Defining Persons

Let's start by defining the people we will need in the policy. To do this, use
the `gittuf policy add-person` command:

```
gittuf person add-person -k <your signing key> --public-key <the public keys of the person>
```

Repeat this as needed for each person that you want to be able to reference in
gittuf policy.

When you are done, let's see where the true power of gittuf shines through,
[writing rules].

[Sigstore]: https://sigstore.dev
[writing rules]: /documentation/maintainers/policy/rules
