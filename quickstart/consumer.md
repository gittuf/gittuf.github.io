---
title: Consumer Quickstart
parent: Installation and Quickstart
layout: default
nav_order: 1
permalink: /quickstart/consumer
---

# Consumer Quickstart

To verify a repository that uses gittuf, you need to first ensure that its
gittuf metadata is available on disk. After you have cloned the repository with
`git clone`, run gittuf in the repository's directory to synchronize its
metadata:

```
gittuf sync
```

Now, determine the branch you would like to verify. Oftentimes, a gittuf policy
will protect the default (e.g. `main`/`master`) branch of a repository. When
you have the branch name, run:

```
gittuf verify-ref <branch name>
```

gittuf will verify that all changes made to the repository have been made in
accordance with the gittuf policy. If there are any errors when verifying,
gittuf will print out an error message to the screen. If there are errors, and
you are sure you have run the above commands properly, you may wish to contact
the repository's maintainers to check the security status of the repository.

If nothing is printed out to the console, then gittuf has successfully verified
the repository against its gittuf policy.

## Next Steps

If you wish to dive deeper into how gittuf can be used to verify repositories,
see the [gittuf Documentation].

[gittuf Documentation]: /documentation
