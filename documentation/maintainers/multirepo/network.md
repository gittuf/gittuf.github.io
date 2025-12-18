---
title: Network Repositories
parent: gittuf Across Multiple Repositories
layout: default
nav_order: 2
permalink: /documentation/maintainers/multirepo/network
---

# Network Repositories

Network repositories are gittuf repositories that inherit a controller's [global
rules].

## Declaring a Controller Repository

On the repository that you want to inherit a controller's global rule policy,
run `gittuf trust add-controller-repository`:

```
gittuf trust add-controller-repository -k <your signing key>
                                       --initial-root-principal <the root principals of the controller repository>
                                       --location <the location of the controller repository>
                                       --name <the name of the controller repository>
```

Add more controller repositories as needed, stage the updated root of trust
metadata, obtain any required signatures from other root of trust users, and
then apply the updated metadata.

{: .info}
> If you read the [Controller Repositories] section, you might have seen
> something very similar to this command before: `gittuf trust
> add-controller-repository`, with the same arguments.
>
> gittuf provides us a special property with a multi-repository architecture.
> Not only can controllers verify that network repositories have genuine
> policies and follow their global rules, but **network repositories can verify
> controller repositories**, e.g. a two-way street of verification. We discuss
> this in more detail below in [Verifying Changes].

## Synchronizing with the Controller

gittuf will automatically fetch any updates to the controller's global rule
policy whenever `gittuf sync` is invoked. There is no need to manually manage
controller metadata.

## Verifying Changes

gittuf verifies the changes made to your repository with the controller's global
rules whenever gittuf verification (e.g. `gittuf verify-ref) is run.

{: .warning}

> A controller repository can set global rules that will cause your repository
> to fail verification. Make sure to inspect the rules that will be applied from
> the controller before adding it.

[global rules]: /documentation/maintainers/root/global-rules
[Controller Repositories]: /documentation/maintainers/multirepo/controller
[Verifying Changes]: #verifying-changes
