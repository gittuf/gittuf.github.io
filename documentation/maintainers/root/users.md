---
title: Managing Users
parent: Root of Trust
layout: default
nav_order: 2
permalink: /documentation/maintainers/root/users
has_toc: no
---

# Managing Users

The root of trust metadata declares both other users in the root of trust, as
well as policy administrators.

## Root of Trust Users

### Adding Additional Root of Trust Users

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

### Removing Root of Trust Users

Should a user need to be removed from the root of trust, you must use the
`remove-key` command:

```
gittuf trust remove-key -k <your signing key> --root-key-ID <the ID of public key of the user to be removed>
```

## Policy Administrators

After adding any other root of trust users, you must add the users authorized to
set gittuf policy for the repository. Because of gittuf's use of TUF
delegations, root users are not automatically policy administrators. Root users
may be also appointed as policy administrators, but this must be explicitly
opted-in to.

### Appointing Policy Administrators

Add the users to be made policy administrators with:

```
gittuf trust add-policy-key -k <your signing key> --policy-ley <the public key of the user to be added>
```

As with the root of trust, gittuf also supports mandating a threshold of policy
administrators agreeing upon changes to be made to the gittuf policy:

```
gittuf trust update-policy-threshold -k <your signing key> --threshold <desired threshold>
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

## Next: Setting Global Rules

Next, we take a look at how the root of trust can set its own rules to protect
the repository in [Global Rules].

[Global Rules]: /documentation/maintainers/root/global-rules
