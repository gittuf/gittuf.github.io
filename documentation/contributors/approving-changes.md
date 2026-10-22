---
title: Approving Changes
parent: 3. gittuf for Contributors
layout: default
nav_order: 5
permalink: /documentation/contributors/approving-changes
---

# Approving Changes with gittuf

If you've used the popular Git forges before, you're likely aware of the
workflow to review and accept (or deny) changes by other users. In the case of
GitHub, you open a pull request, and then reviewers add their thoughts and
either approve your changes, or request edits from you.

gittuf enables a similar workflow, where users can approve changes that you made
to be merged into another branch with the **approval workflow**. Let's take a
look at how it works.

## Approval Workflow

Let's say you want to merge your changes from the `feature` branch (which is not
protected by gittuf policy), into the `main` branch (which is protected by
gittuf policy). The policy requires that at least two users approve any change
to the `main` branch.

If you are authorized to make changes to the main branch, your signature on the
merge commit merging your changes would count for one signature.

However, you'd still need one more user to sign off with their approval. To do
this, after you have pushed your changes to the `feature` branch, the other user
must first pull them down.

After the user examines the changes and is content with them, gittuf provides a
command `gittuf attest authorize` to indicate approval to merge changes in. To
do this, the user will run:

```
gittuf attest authorize --from-ref <branch to merge from> <branch to merge into>
```

gittuf will then record the user's approval as an attestation, and will upload
it to the remote server for you to pull back down with `gittuf sync`.

Now that the required approvals have been added, you can merge the changes with
`git merge`:

```
git checkout main
git merge feature
```

Now, your changes will appear in the `main` branch, and will successfully
verify. If additional users are required to approve changes, they may do so by
running the `gittuf attest authorize` command before you merge your changes in.

## Using the RSL to Approve Changes

Recording changes in the RSL is another way that changes may be approved, though
this is subject to the restriction that the approval using the RSL must be the
last approval required.

For example, if two out of three approvals are recorded for merging a change to
`main`, a user trusted for the `main` branch may go ahead and merge the change,
so as long as they record the update to the `main` branch with one of their keys
authorized to make changes to `main`.

## Next: Administering gittuf

We've now seen how contributors can use gittuf on a day-to-day basis. Let's now
take a look at how gittuf policies are created so we can actually protect the
repository in [Part 4: gittuf for Maintainers].

[Part 4: gittuf for Maintainers]: /documentation/maintainers
