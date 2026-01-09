---
title: Global Rules
parent: Root of Trust
layout: default
nav_order: 1
permalink: /documentation/maintainers/root/global-rules
---

# Global Rules

[gittuf policy] allows administrators to compose a security policy to protect
their repositories. Because the users that make up the root of trust are not
automatically made Policy Administrators, these users do not have any direct say
about how the policy in a repository should be structured.

**Global Rules** address two key shortcomings with regular gittuf policy:

1. Global Rules allow root of trust users to specify a _baseline_ policy that
   must be met, regardless of how lenient the gittuf policy is.
2. Global Rules are generalized, and therefore are not necessarily tied to any
   one gittuf repository. We discuss this point further in [gittuf Across
   Multiple Repositories].

There are two types of global rules. Let's take a look at each of them.

## Block Force-Pushes Rule

Force-pushing in Git allows a user to rewrite the history of a branch, by
pushing changes that do not necessarily have the same history currently on the
branch. This is useful, but also has obvious security implications.

The **Block Force-Pushes** global rule type instructs gittuf to fail
verification should the branch being verified have been force-pushed.

## Minimum Threshold Rule

The **minimum threshold** global rule type is simply that; a rule which requires
that a certain threshold of users be required to make a change to a Git
reference or file/folder. Unlike thresholds in gittuf policy, the global rule
**does not** stipulate the specific users that can count towards the threshold.

Instead, trusted users are determined in the gittuf policy as usual, and during
verification, both the policy rule and global rule are evaluated.

For example, even if Alice and Bob both sign a change to meet a policy rule with
a threshold of two, a global rule that requires that change be signed with three
users will cause that change to fail verification.

## Creating Global Rules

Because global rules reside in a repository's root of trust metadata, only root
of trust users may create and modify them. Global rules follow a similar
creation process to that of [policy rules]. The command for adding a global rule
is the same for both types of global rules, but its invocation varies.

To add a threshold global rule, run:

```
gittuf trust add-global-rule -k <your signing key>
                            --type threshold
                            --threshold 1
                            --rule-pattern <rule pattern>
```

To add a block force-pushes global rule, run:

```
gittuf trust add-global-rule -k <your signing key>
                             --type block-force-pushes
                             --rule-pattern <rule pattern>
```

{: .info}

> Global rules require a rule pattern just like rules defined in gittuf policy.
> A threshold global rule can accept a rule pattern of either `git:` or `file:`,
> but a block force-pushes global rule can only accept a `git:` rule pattern.

[gittuf policy]: /documentation/maintainers/policy
[gittuf Across Multiple Repositories]: /documentation/maintainers/multirepo
[policy rules]: /documentation/maintainers/policy/rules
