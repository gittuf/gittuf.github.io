---
title: Supported Operations
parent: Root of Trust
layout: default
nav_order: 2
permalink: /documentation/maintainers/root/operations
---

# Supported Operations

## Root of Trust Management

The following operations are supported for root of trust management in gittuf.

### Initialization (`gittuf trust init`)

Before any other operation can occur in gittuf, the root of trust must be itself
initialized. To do so, run:

```
gittuf trust init -k <your signing key>
```

{: .info}

> The root of trust may only be initialized once. If you want to re-initialize
> gittuf's metadata, you must [reset gittuf] on your repository.


### Adding Root of Trust Users (`gittuf trust add-root-key`)

Should other users need to be added to the root of trust, you must use the
`add-key` command to do so:

```
gittuf trust add-key -k <your signing key> --root-key <the public key of the user to be added>
```

### Removing Root of Trust Users (`gittuf trust remove-root-key`)

Should a user need to be removed from the root of trust, you must use the
`remove-key` command:

```
gittuf trust remove-key -k <your signing key> --root-key-ID <the ID of public key of the user to be removed>
```

### Setting a Root of Trust Threshold (`gittuf trust update-root-threshold`)

By default, gittuf sets the threshold of users required to make changes to the
root of trust to one. To update this, you must use the `update-root-threshold`
command:

```
gittuf trust update-root-threshold -k <your signing key> --threshold <desired threshold>
```

{: .info}

> The threshold cannot be greater than the total number of users currently
> defined in the root metadata, i.e. you must add all users first before setting
> the threshold.

### Adding Policy Administrators (`gittuf trust add-policy-key`)

As the root of trust appoints the policy administrators, they must be declared
when configuring the root of trust:

```
gittuf trust add-policy-key -k <your signing key> --policy-key <the administrator's public key>
```

### Removing Policy Administrators (`gittuf trust remove-policy-key`)

To remove a policy administrator, run:

```
gittuf trust remove-policy-key -k <your signing key> --policy-key-ID <the administrator's public key ID>
```

### Setting a Policy Administrator Threshold (`gittuf trust update-policy-threshold`)

Much like the root of trust, gittuf also supports requiring a threshold of
Policy Administrators to agree upon changes to the gittuf policy. To set this
threshold, run:

```
gittuf trust update-policy-threshold -k <your signing key> --threshold <desired threshold>
```

### Signing (`gittuf trust sign`)

If the threshold of users for the root of trust is greater than one, then
multiple users must approve the changes made to the root of trust. Every user to
approve (except the user that originally made the changes) must invoke the
`sign` command.

```
gittuf trust sign -k <user's signing key>
```

### Staging, Applying, and Rolling Back (`gittuf trust stage`, `gittuf trust apply`, and `gittuf trust discard`)

Changes to the root metadata are not effective instantly, to prevent lockouts,
for allowing changes to be rolled back if desired, and to allow for all required
signatures to be obtained.

When you are finished with configuring the desired root of trust, you must
_stage_ your changes:

```
gittuf trust stage <remote name>
```

{: .info}

> By default, the command will require a remote server to be
> specified so that changes can be pushed automatically. To only stage your
> changes locally (e.g. if you are not using a remote server), use `--local-only`.
>
> ```
> gittuf trust stage --local-only
> ```

Now, other users must pull the changes down and sign your changes to meet the
required threshold. Once this is complete (or you are the only root of trust
user/the threshold is one), the changes must be _applied_, i.e. made
enforceable:

```
gittuf trust apply <remote name>
```

The same behavior with `--local-only` in `gittuf trust stage` detailed above
applies for `gittuf trust apply`.

### Additional Data 

The root of trust also encodes additional repository data.

#### Repository Location

To set the canonical repository location, i.e. the server where the
"main"/working copy of your repository can be found, use the `gittuf trust
set-repository-location` command:

```
gittuf trust set-repository-location -k <your signing key> --location <repository location URL>
```

Note that this does not grant this copy of the repository any special
privileges, it simply records it so that users may know where to obtain the
canonical copy from.

## Global Rules

gittuf also supports rules defined directly in the root of trust metadata. These
rules are called global rules, and 

For more information on declaring these rules, see the [documentation for global
rules].

[reset gittuf]: /documentation/maintainers/uninstalling#resetting-gittuf
[documentation for global rules]: /documentation/maintainers/root/global-rules
