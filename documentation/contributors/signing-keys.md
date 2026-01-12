---
title: Signing Keys
parent: 3. gittuf for Contributors
layout: default
nav_order: 1
permalink: /documentation/contributors/signing-keys
---

# Signing Keys

In Git, committers (or their authors) are usually identified by two pieces of
metadata:

- the committer's / author's name, and,
- the committer's / author's email

It's trivial to spoof the name and email on a new commit, simply just choose the
person you'd like to impersonate and set their details on your computer as you
would with your name and email in Git.

Because of this, we cannot rely on these pieces of information alone, and need a
stronger guarantee of someone's identity. To that end, gittuf uses [Git's native
commit signing feature].

## Generating Your Keys

If you already have a GPG key, SSH key, or [Sigstore] identity that you want to
use for Git commit signing, skip to [Setting Up Your Keys]. Otherwise, we
suggest following GitHub's article on generating a [GPG key] or an [SSH key] for
use in Git.

## Setting Up Your Keys

Next, change your working directory to be the Git repository you would like to
configure your signing keys for. Run the instructions below for the appropriate
key type you are using:

{: .info}

> If you would like to only configure these settings once for all Git
> repositories on your computer, replace the `--local` flag with `--global`.

### GPG

```
git config --local commit.gpgsign true
git config --local tag.gpgsign true
git config --local user.signingkey <your GPG key's fingerprint>
```

### SSH

```
git config --local commit.gpgsign true
git config --local tag.gpgsign true
git config --local gpg.format ssh
git config --local user.signingkey <path to your SSH key>
```

### Sigstore

```
git config --local commit.gpgsign true
git config --local tag.gpgsign true
git config --local gpg.format x509
git config --local gpg.x509.program gitsign
```

## Next: Automatic Push Recording

Now, let's see how gittuf can automatically handle recording pushes and updates
to its metadata in the background of your daily workflow with [Automatic Push
Recording].

[Git's native commit signing feature]: https://git-scm.com/book/en/v2/Git-Tools-Signing-Your-Work
[Sigstore]: https://sigstore.dev
[GPG Key]: https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key
[SSH Key]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent
[Setting Up Your Keys]: #setting-up-your-keys
[Automatic Push Recording]: /documentation/contributors/automatic
