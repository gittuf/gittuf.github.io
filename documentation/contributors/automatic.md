---
title: Automatic Metadata Management
parent: 3. gittuf for Contributors
layout: default
nav_order: 2
permalink: /documentation/contributors/automatic
has_toc: no
---

# Automatic Metadata Management

gittuf ships with a program (`git-remote-gittuf`) known as a _Git remote
helper_, which is used by your computer to talk with Git servers (e.g. GitHub,
GitLab, Bitbucket, etc...). Because of this, it must be invoked every time you
run commands such as `git pull` or `git push`, and serves as a reliable place to
run common gittuf tasks. The transport automatically does the following for you:

- Create [RSL Entries] as needed
- Synchronize gittuf metadata
- [Verify that the repository is compliant with gittuf policy]

This means that you need not interact with gittuf to do the work you already do
on your Git repository. **There is one exception: [Approving Changes] with
multiple users required.**

{: .info}

> If you are a maintainer, you can use the gittuf transport, but will still need
> to interact with gittuf manually to set policies. See [Part 4: gittuf for
> Maintainers] for more information.

Automatic metadata management is performed whenever you are interacting with a
Git remote whose URL has `gittuf::` prepended to it.

For example, if you push to GitHub using `https`, your Git remote will be:

```
https://github.com/user/repository.git
```

If we wanted to use automatic metadata management for gittuf for this
repository, we need to only add `gittuf::` to the beginning of this URL, like
so:

```
gittuf::https://github.com/user/repository.git
```

## Enabling Automatic Metadata Management

If you haven't cloned the repository you need to work on yet, simply add the
`gittuf::` prefix to the URL where your Git repository is located. For example,

```
git clone gittuf::git@github.com:owner/repo
```

If you have cloned the repository you need to work on, navigate to it, and then
update the remote server URL from which you fetch changes from. For example,
if your default server is `origin` (in most cases), run:

```
git remote set-url origin gittuf::git@github.com:owner/repo
```

## Disabling Automatic Metadata Management

Disabling gittuf's automatic metadata management for a repository simply
requires removing the `gittuf::` prefix from the remote URL. For example, if
your default server is `origin`, run:

```
git remote set-url origin git@github.com:owner/repo
```

## Next: Manual Metadata Management

Next, let's take a look at how gittuf metadata is managed manually, without
`git-remote-gittuf` with [Manual Metadata Management].


[RSL Entries]: /documentation/contributors/metadata
[Verify that the repository is compliant with gittuf policy]: /documentation/consumers/verifying
[Approving Changes]: /documentation/contributors/approving-changes
[Part 4: gittuf for Maintainers]: /documentation/maintainers
[Manual Metadata Management]: /documentation/contributors/manual
