---
title: Controller Repositories
parent: gittuf Across Multiple Repositories
layout: default
nav_order: 1
permalink: /documentation/maintainers/multirepo/controller
---

# Controller Repositories

Controller repositories are gittuf repositories that declare some set of [global
rules] to be reused by other gittuf repositories. The controller attribute is
opt-in, and must be configured by the root of trust users.

## Enabling a Controller Repository

On the repository that you want to enable controller functionality on, run
`gittuf trust make-controller`:

```
gittuf trust make-controller -k <your signing key>
```

Stage the updated root of trust metadata, obtain any required signatures from
other root of trust users, and then apply the updated metadata. The repository
will now be enabled as a controller and other repositories will be able to
utilize the global rule policy declared by the controller repository.

{: .heads-up}

> Any user who can pull from the controller repository will be able to inherit
> its global rules. If you would like to limit access to the controller, you
> must apply these controls at the network or platform level (e.g. block access
> to the controller or make it private on a forge). gittuf cannot block access.

## Adding Network Repositories

By default, a controller repository takes a passive role and simply allows its
policy to be inherited by other gittuf repositories. This is ideal for scenarios
where a controller serves as a public-good global rule "template" for any
arbitrary repository to use.

For enterprises where compliance must be _enforced and verified_, gittuf
includes a mechanism to declare downstream repositories that must declare and
inherit the policy of a controller. We call these repositories **network
repositories**.

To add a network repository, use the `gittuf trust add-network-repository`
command:

```
gittuf trust add-network-repository -k <your signing key>
                                    --initial-root-principal <the root principals of the network repository>
                                    --location <the location of the network repository>
                                    --name <the name of the network repository>
```

To ensure that the network repository's metadata is genuine, you must supply the
**initial** root principals, i.e. the root principals in the first applied state
of gittuf metadata. You must also supply the location of the repository, which
is normally a URL of the canonical location (e.g. a link to the GitHub
repository). Finally, the name of the repository is required to identify this
repository in verification reports.

Add more network repositories as needed, stage the updated root of trust
metadata, obtain any required signatures from other root of trust users, and
then apply the updated metadata.

## Verifying Network Repositories

Once you have added the appropriate network repositories and applied the changes
to the root of trust metadata, you can now check that these network repositories
have properly inherited your controller's global rules. This is done using the
`gittuf verify-network` command:

```
gittuf verify-network
```

{: .info}

> Verification of network repositories is an operation that requires pull access
> to all network repositories. Ensure that you have network or disk access to
> all network repositories before invoking verification to ensure that
> verification does not fail.

gittuf will clone all network repositories, verify their metadata, and verify
that they declare the controller repository properly. gittuf will then verify
that all commits in the network repository adhere to the global rules declared
in the controller repository.

If a verification failure occurs, gittuf will output an error message to the
console.

## Next: Network Repositories

Let's see a multi-repository gittuf deployment from the other type of repository
in it, [Network Repositories].

[global rules]: /documentation/maintainers/root/global-rules
[Network Repositories]: /documentation/maintainers/multirepo/network
