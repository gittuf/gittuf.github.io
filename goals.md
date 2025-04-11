---
title: Goals
layout: default
nav_order: 2
---

In building gittuf, we have several specific goals that determine specific
design decisions. A detailed description of how gittuf accomplishes these goals
can be found in the living [design document].

## Independent Policy Verification

A primary goal for gittuf is to enable independent verification of a
repository's security policies. Today, repository security is typically left to
the source control platform (SCP). While SCPs provide valuable security features
(many of which we use in developing gittuf!), they serve as a single point of
trust in the software supply chain, as the platform is the only entity capable
of setting and enforcing a repository's policies. A compromised SCP or Git
server can allow attackers to push malicious changes, bypassing the configured
security controls.

**How does gittuf accomplish this goal?** gittuf policy metadata is stored in
the repository. gittuf also uses public key cryptography to authenticate
developers. Thus, any developer who can read from the repository can use the
gittuf tool to verify the policies were followed for the repository's changes.

## Guardrails for Policy Declaration

Git security policies provide guardrails for how changes can be made to the
repository and by whom. gittuf aims to provide similar guardrails for how the
policies themselves are declared and updated. For example, a repository hosted
on an SCP may use the SCP's features to require at least two maintainers to
approve all changes to the `main` branch. But, if a single maintainer can
_disable_ the rule requiring two approvals for changes to the `main` branch,
then a single maintainer (or an attacker who compromises a maintainer!) can
bypass this control.

**How does gittuf accomplish this goal?** gittuf policy can be configured to
require a minimum number of approvals for changes to repository contents _and_
gittuf policy metadata itself. gittuf also adds other guardrails for how
developers can amend policy using _delegations_. A developer can be trusted to
amend the policy to add other trusted developers (i.e., to delegate), but only
for _portions of the repository the developer is already trusted for_. This
mitigates situations where a large number of developers are granted more
permissions than they need, common in larger repositories.

## Protections for Repository Activity Logs

Logs are vital to reasoning about the repository's security, especially to
triage incidents. Much like policy enforcement, repository logs are typically
the responsibility of the SCP. gittuf aims to protect these logs from tampering
(e.g., dropping an action from the log, reordering activity in the repository).
After all, if an attacker compromises an SCP to undermine a repository's
policies, they can also tamper with the audit logs to hide their traces.

**How does gittuf accomplish this goal?** Much like the gittuf policy,
repository activity information is also stored in the repository itself. The log
is append-only and records pushes as well as other types of actions such as code
review approvals. The log is synchronized across all copies of the repository by
the gittuf client. Thus, to tamper with a repository's activity log, an attacker
must tamper with the log in all copies of the repository, _including on
individual developer machines_.

## {system}-Agnostic and Backwards Compatible

Developers have many different ways of writing code. There isn't a
one-size-fits-all solution. Therefore, gittuf aims to remain as unopinionated
and {system}-agnostic as possible, and to be compatible with popular Git tooling
like code review tools and SCPs.

**How does gittuf accomplish this goal?** gittuf stores all of its additional
metadata using native Git semantics like its object store and references. This
allows gittuf to be used with any standard Git repository, including existing
repositories! gittuf also supports a variety of signing mechanisms such as GPG,
SSH keys, and [Sigstore] [gitsign].

[design document]: https://github.com/gittuf/gittuf/blob/main/docs/design-document.md
[Sigstore]: https://sigstore.dev
[gitsign]: https://github.com/sigstore/gitsign
