---
title: Root of Trust
parent: 4. gittuf for Maintainers
layout: default
nav_order: 2
permalink: /documentation/maintainers/root
has_toc: no
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

## Initialization

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

## (Optional) Adding Additional Users

After you have initialized the root of trust metadata, you can add additional
users, and adjust the threshold of users required to sign changes to the root of
trust metadata. You will need to have the public key files of the users to be
added.

To add users, run the following command for as many users as there are to be
added:

```
gittuf trust add-root-key -k <your signing key> --root-key <the public key of the user to be added>
```

After you have added the other users, you can adjust the root threshold as
follows:

```
gittuf trust update-root-threshold -k <your signing key> --threshold <desired threshold>
```

## Appointing Policy Administrators

Now, you must add the users authorized to set gittuf policy for the repository.
Because of gittuf's use of TUF delegations, root users are not automatically
policy administrators. Root users may be also appointed as policy
administrators, but this must be explicitly opted-in to.

Add the users to be made policy administrators with:

```
gittuf trust add-policy-key -k <your signing key> --policy-ley <the public key of the user to be added>
```

As with the root of trust, gittuf also supports mandating a threshold of policy
administrators agreeing upon changes to be made to the gittuf policy:

```
gittuf trust update-policy-threshold -k <your signing key> --threshold <desired threshold>
```

## Signing and Applying the Root Metadata

Once you have added the desired users to the root of trust and appointed the
policy administrators, the root of trust must be signed and made active.

This process varies depending on whether other root of trust users must sign
your changes.

### I'm the Only Root of Trust User / Threshold of One

If you are the only root of trust user, or the root (not policy) threshold is
set to one, then the process is easy.

First, _stage_ the changes with `gittuf trust stage`. If your default remote is
`origin` (as is in most cases), run:

```
gittuf trust stage origin
```

This will automatically push your changes to the remote. If you do not wish to
do so, append `--local-only`:

```
gittuf trust stage --local-only
```

Next, _apply_ the changes with `gittuf trust apply`. `apply` uses the same
`--local-only` semantics as `stage`:

```
gittuf trust apply origin
```

gittuf will make your changes to the root of trust active and enforceable. These
changes will be reflected in `refs/gittuf/policy`.

### Multiple Users Must Approve Changes / Threshold > 1

If other root of trust users must sign your changes before they are valid, the
process is a bit more involved.

First, _stage_ the changes with `gittuf trust stage`. If your default remote is
`origin` (as is in most cases), run:

```
gittuf trust stage origin
```

gittuf will push the changes to the remote. Now, other users must pull the
changes to their computers to sign them.

The other users must tell gittuf to pull down the changes made to the root of
trust metadata:

```
gittuf sync
```

Now, the other users must each sign the changes with `gittuf trust sign`:

```
gittuf trust sign -k <the user's signing key>
```

Finally, each user must sync their changes after signing with `gittuf sync`.

When all users have signed off on the changes to the root of trust, you can
finish the process and make the changes live with:

```
gittuf trust apply origin
```

gittuf will make your changes to the root of trust active and enforceable. These
changes will be reflected in `refs/gittuf/policy`.

## Next Steps

gittuf's root of trust is now set up! Now, let's take a look at how setting a
policy works in [Policy].


[global rules]: /documentation/maintainers/root/global-rules
[reset gittuf]: /documentation/maintainers/uninstalling#resetting-gittuf
[Policy]: /documentation/maintainers/policy
