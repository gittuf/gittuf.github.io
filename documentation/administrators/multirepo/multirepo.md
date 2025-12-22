---
title: gittuf Across Multiple Repositories
parent: 4. Administering gittuf
layout: default
nav_order: 4
permalink: /documentation/administrators/multirepo
---

# gittuf Across Multiple Repositories

The original design of gittuf only allowed applying gittuf controls over a
single Git repository. While this is sufficient for many repositories,
organizations often have multiple (and sometimes, thousands!) of Git
repositories to manage. Managing each repository's security policy can become an
impossible task.

Likewise, foundations and authorities (e.g. TODO) set best-practices for
software developers to follow (e.g. multi-party code review, protecting the
default branch of a Git repository from force-pushes, etc...).

To address these limitations, gittuf was extended to allow for gittuf policies
to **be applied over multiple repositories**. We call this **multi-repository**
support.

## Multi-Repository Architecture

gittuf's multi-repository architecture can be compared to the organizational
features provided by popular forges today (e.g. GitHub Organizations). Unlike
these features however, gittuf is much more flexible. To understand how gittuf
implements support for spanning across multiple repositories, let's look at the
building blocks.

### Global Rules

Any gittuf repository may create a _global rule policy_. Global rules are simply
gittuf rules that are defined at the root of trust instead of in the policy.
When used in a single gittuf repository, these rules apply _in addition to_ any
rules defined in the policy.

This means that global rules establish a _minimum baseline_ that must be
followed for the parts of the repository that they cover.

Global rules can be one of two types:

1. **Threshold rules**, which stipulate a minimum number of users that must
   approve changes to a specific part of the repository (but do not specify
   **who** those users must specifically be).
2. **Block force push rules**, which prevent users from force pushing over
   protected references in Git.

The policy for a repository may set stricter rules, but the global rules will
be the minimum bar that each change to the parts of the repository they
protect must meet.

### Controller Repositories

Because global rules do not specify specific users in their configuration, they
are easy to apply across different repositories that may have different sets of
users (mandating that three trusted users approve a change can be met by any
repository that defines three users authorized to make changes).

With gittuf, a repository can contain a configuration of global rules, intended
to be applied and enforced over an arbitrary set of other repositories. We call
this repository a **controller repository**.

Once a repository is enabled as a controller, any other gittuf repository can
inherit its global rules (but not any policy rules). This means that a
controller repository can be simply used for creating rules (e.g. a "good
practices rules" repository), or also used for development itself (e.g. an
organization's "management repository").

Controller repositories can also inherit global rules from any arbitrary set of
other controller repositories, making it possible to "collect" multiple sets of
global rules into one place. From here, an organization can simply add this
"collection repository" as a controller for all of their internal repositories.

### Network Repositories

To reuse a controller's global rule policy, a repository need not be explicitly
declared as a consumer by the controller. For repositories that aim to provide
"good practices rules", the consumers may be a huge set of unrelated
repositories from multiple owners and organizations, and it would be impossible
to manually approve all consumers.

However, for organizations that wish to not only _set_ a baseline policy, but
also _automatically verify compliance_ with the baseline policy across all their
repositories, the **network repository** comes into play.

A controller can define network repositories, which are repositories that are
expected to declare the controller repository as such in their root of trust
metadata.

The root of trust users of the controller repository can then invoke gittuf to
automatically fetch each network repository, and verify that these repositories
indeed have:

- declared the controller
- followed the global rules appropriately

gittuf performs this automatically and, upon completion, reports the
repositories that are in compliance, and those that are not.

[Controller Repositories]: /administrators/multirepo/controller
[Network Repositories]: /administrators/multirepo/network
