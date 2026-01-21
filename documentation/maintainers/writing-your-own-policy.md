---
title: Writing your own gittuf Policy
parent: 4. gittuf for Maintainers
layout: default
nav_order: 6
permalink: /documentation/maintainers/policy/own
---

# Writing Your Own gittuf Policy

After reading the documentation for gittuf, you may be wondering, "How do I
write my own gittuf policy?"

While every repository has different security requirements, there are certain
best practices that are good starting points for you to build your policy on. On
this page, we detail some resources to help you with doing so.

## What Should I Protect?

You likely need not protect every branch in your Git repository. If only the
`main` branch, for instance, is used to build releases for your project (which
are then tagged), then your policy can be as simple as:

- Protect the `main` branch (`git:refs/heads/main`), and only allow maintainers
  to commit directly to the branch, preferably with a threshold greater than
  one.
- Protect the release tags (e.g. `git:refs/tags/v*` or whatever format you use)
  with a tag protection rule that only allows maintainers, (or a subset of
  maintainers) to create releases.

With these two rules, any release of your project will need to comply with the
gittuf policy, even if development occurs in unprotected feature branches, e.g.
`development`, `feature`, etc., as the changes in these branches must be merged
into the protected `main` branch.

## Applying the Policy in gittuf

Once you've formulated the policy that you'd like to apply, you will need to
tell gittuf how to apply it. In addition to this documentation, we have various
demos of gittuf functionality available on our [demo website].

These demos apply various example policies. For instance, there is a [basic
demo], which shows how a gittuf policy can be applied from initializing gittuf,
to enforcing it and verifying changes. There is also a [multi-repository demo],
which showcases the multi-repository features discussed earlier.

[demo website]: https://github.com/gittuf/demo
[basic demo]: https://github.com/gittuf/demo/blob/main/demo.md
[multi-repository demo]: https://github.com/gittuf/demo/blob/main/demo-multi-repo.md
