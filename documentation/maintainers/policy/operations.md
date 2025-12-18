---
title: Supported Operations
parent: Policy
layout: default
nav_order: 4
permalink: /documentation/maintainers/policy/operations
---

# Supported Operations

## General Policy Management

The following operations are supported for general management of the gittuf
policy.

### Policy Initialization (`gittuf policy init`)

Before rules may be created in a policy, the policy must first be initialized.
To initialize the main gittuf policy, run:

```
gittuf policy init -k <your signing key>
```

Unlike the root of trust metadata, gittuf supports multiple policy files. By
default, the initialization command creates the primary policy, but the policies
used by Delegated Policy Administrators must be initialized separately. The
`gittuf policy init` command supports initializing separate policy files with
the `--policy-name` flag, like so:

```
gittuf policy init -k <your sigining key> --policy-name <delegated policy name>
```

## Operations for Principals

The following operations are supported for managing principals (of all types) in
gittuf policy:

### Listing Defined Principals (`gittuf policy list-principals`)

You can list all the persons currently defined in gittuf metadata:

```
gittuf policy list-principals
```

## Operations for Persons

The following operations are supported for managing persons in gittuf policy:

### Adding a Person (`gittuf policy add-person`)

Add a person to the gittuf policy.

```
gittuf policy add-person --person-ID <person identifier> --public-key <the public keys of the person>
```

### Removing a Person (`gittuf policy remove-person`)

To remove a person from gittuf policy, use their person ID:

```
gittuf policy remove-person --person-ID <person identifier>
```

{: .heads-up}

> The person must not currently be referenced by any rule in the policy,
> otherwise gittuf will raise an error.

### Updating a Person (`gittuf policy update-person`)

Persons currently defined in gittuf policy can be updated:

```
gittuf policy update-person --person-ID <person identifier> --public-key <the public keys of the person>
```

{: .heads-up}

> The details specified for the person in this command will **replace** the
> current data, so make sure to define all existing signing keys that you wish
> to keep associated with the person.
