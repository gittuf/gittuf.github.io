---
title: Contributor and Maintainer Quickstart
parent: Installation and Quickstart
layout: default
nav_order: 2
permalink: /quickstart/contributor-maintainer
---

# Contributor and Maintainer Quickstart

{: .experimental}

> The `gittuf setup` utility is not yet a part of gittuf, but can be run by
> building the code from [PR #1124].

Ensure that you are in the directory of the repository you want to use with
gittuf. Next, ensure that you have set your signing key in Git (see [Signing
Keys] for more information or help).

Finally, invoke the `gittuf setup` utility with your role below. Make sure to
also read [Finishing Setup].

## Contributors

If you are a contributor, run:

```
gittuf setup contributor
```

The utility will check if a maintainer has already set up gittuf on the
repository. If gittuf has not been yet setup, the utility will inform you to
check with a maintainer to ensure that they have set up gittuf.

## Maintainers

If you are a maintainer, run:

```
gittuf setup maintainer
```

The utility will check if gittuf has already been set up on the repository. If
it has not, the utility will initialize gittuf and prompt you to create a basic
policy that:

- adds you to the root of trust, and,
- creates a rule that authorizes you to commit to the default branch of the
  repository.

If gittuf _has_ already been set up, the utility will ask you to confirm that
this is intended, to ensure that a user has not set up gittuf maliciously.

## Finishing Setup

The last step the utility will take, regardless of your role, is to offer setup
of [Automatic Push Recording], where gittuf automatically records your
changes/pushes, synchronizes its metadata with the remote server, and
automatically verifies any new changes you pull from the server.

For more information on how this works, see [Automatic Push Recording]. If you
prefer instead to manually record your pushes and verify the repository, please
read [Manual Push Recording].

## Next Steps

If you are a contributor, that's all there is to using gittuf on a daily basis.
Unless you prefer to poke around, gittuf should stay out of your way. If it
doesn't, please [open an issue] on our issue tracker so we can investigate.

If you're a maintainer or a more hands-on user interested in poking around with
gittuf, see the [gittuf Documentation].

[PR #1124]: https://github.com/gittuf/gittuf/pull/1124
[Signing Keys]: /documentation/contributors/signing-keys
[Finishing Setup]: #finishing-setup
[Automatic Push Recording]: /documentation/contributors/automatic
[Manual Push Recording]: /documentation/contributors/manual
[open an issue]: https://github.com/gittuf/gittuf/issues/new
[gittuf Documentation]: /documentation
