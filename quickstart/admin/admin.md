---
title: Administrator Quickstart
parent: Quickstart
layout: default
nav_order: 2
permalink: /quickstart/admin
---

# Administrator Quickstart

gittuf contains a setup wizard that will get you started with a basic security
policy that you can build on as needed. 

{: .info }

> If you are starting with a new Git repository, make sure to initialize it with
> `git init -b <branch name>` before proceeding.

## Signing Keys

First, configure your signing keys in Git. If you already have a GPG, SSH, or
[Sigstore] key that you use, configure it as below. If you do not already have a
key, follow the **Sigstore** instructions.

GPG:

{: .heads-up}

> At the moment, you must have an SSH or Sigstore key to manage gittuf, but you
> can still use a GPG key to sign your commits.

```
git config --local commit.gpgsign true
git config --local tag.gpgsign true
```

SSH:
```
git config --local commit.gpgsign true
git config --local tag.gpgsign true
git config --local gpg.format ssh
git config --local user.signingkey <path to your SSH key>
```

Sigstore:
```
git config --local commit.gpgsign true
git config --local tag.gpgsign true
git config --local gpg.format x509
git config --local gpg.x509.program gitsign
```

## Configuration

After you have configured your signing keys, run the setup wizard to configure a
basic gittuf policy:

```
gittuf setup
```

gittuf is now set up on your repository.

## Daily Workflow

If you plan to push your repository to a service such as GitHub, gittuf can
automatically handle recording and verifying commits. Simply add the `gittuf::`
prefix to your repository's remote URL, e.g. `git@github.com:owner/repo` becomes
`gittuf::git@github.com:owner/repo`.

You can update your Git configuration with this change as follows:
```
git remote set-url origin gittuf::git@github.com:owner/repo
```


## Verifying Changes

To verify that the gittuf policy was followed on the repository, run:

```
gittuf verify-ref <branch name>
```

## Next Steps

If you'd like to learn more about how gittuf works or adjust gittuf's security
policy to better fit your needs, see the [Administering gittuf guide].

[Sigstore]: https://sigstore.dev
[Administering gittuf guide]: /documentation/administrators
