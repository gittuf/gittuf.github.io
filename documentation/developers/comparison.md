---
title: Comparison with Other Systems
parent: 5. gittuf for Developers
layout: default
nav_order: 2
permalink: /documentation/developers/comparison
---

# Comparison with Other Systems

In this page, we compare gittuf with other systems that address Git repository
security, commit authentication, and policy enforcement. The comparison criteria
are directly drawn from [gittuf's goals](https://gittuf.dev/goals.html).

The systems being compared here are [Guix's git authentication
model](https://guix.gnu.org/en/blog/2024/authenticate-your-git-checkouts/) and
[sequoia-git](https://sequoia-pgp.gitlab.io/sequoia-git/). Both these models
share gittuf's core principle of representing all authentication information
directly in the repository, independent of any forge or third-party authority.

The areas where gittuf differs most from the other 2 systems reflect its broader
scope: multi party threshold authorization, an append-only activity log and
forge integration.

---

## Independent Policy Verification

This is the ability for any developer to independently verify that a
repository's changes followed the expected security policies, without relying on
a **source control platform (SCP)** such as GitHub, GitLab, or Bitbucket.

| | gittuf | Guix | sequoia-git |
|---|---|---|---|
| **Authentication data stored in the repository** | Yes: policy metadata, RSL entries, and attestations are stored as native Git objects | Yes: `.guix-authorizations` and the `keyring` branch are stored in the repository | Yes: `openpgp-policy.toml` and certificates are stored in the repository |
| **Verification independent of SCP** | Yes: any developer with read access can run `gittuf verify-ref` | Yes: `guix git authenticate` runs locally with no forge dependency | Yes: `sq-git log` runs locally with no forge dependency |
| **Protection if SCP is compromised** | Yes: policy and activity log are in the repository, a compromised SCP cannot silently bypass controls | Yes: `.guix-authorizations` changes require an authorized maintainer signature; SCP cannot override | Yes: policy changes require an authorized signer per `openpgp-policy.toml`; SCP cannot override |
| **Cryptographic signing backends supported** | GPG, SSH keys, Sigstore/gitsign | GPG only | GPG only |
| **Keyless / OIDC-based signing** | Yes: via Sigstore integration | No | No |

---

## Guardrails for Policy Declaration

This is the ability of the tools to protect how policies themselves are declared
and updated, preventing a single party from unilaterally changing the rules.

| | gittuf | Guix | sequoia-git |
|---|---|---|---|
| **Threshold approvals required for policy changes** | Yes: configurable minimum number of signatures required to update policy | No: any single authorized maintainer can update `.guix-authorizations` | No: the policy owner can update `openpgp-policy.toml` unilaterally |
| **Fine-grained delegation** | Yes: a developer can be delegated trust for specific paths or refs only, and can only sub-delegate within their scope | No: any authorized maintainer can touch any file | Partial: roles can be scoped by change type (commits, releases, policy) but not by file path |
| **Policy history is versioned and verifiable** | Yes: the RSL records every policy change with the signatures that authorized it | Partial: policy file changes are git-signed commits but not recorded as separate attestations in an independent log | Partial: policy file changes are git-signed commits but not recorded as separate attestations in an independent log |
| **Minimum trust required to change who is trusted** | Yes: adding a maintainer requires meeting the threshold of the existing trusted set | No: any existing authorized maintainer can add or remove others | No: any existing authorized signer can add or remove others |

---

## Protections for Repository Activity Logs

This is the ability to maintain a tamper-evident log of all repository activity
that cannot be silently dropped, reordered, or modified.

| | gittuf | Guix | sequoia-git |
|---|---|---|---|
| **Append-only activity log** | Yes: the Reference State Log (RSL) is an append-only structure recording all pushes, policy changes, and attestations | No: relies on standard git history, which can be rewritten | No: relies on standard git history, which can be rewritten |
| **Logs synchronized across all repository copies** | Yes: the RSL is synchronized across clones by the gittuf client; tampering requires altering every copy | No | No |
| **Logs record code review approvals** | Yes: attestations for PR approvals are recorded in the RSL | No | No |
| **Protection against log reordering or entry drops** | Yes: RSL entries form a chain; dropping or reordering entries breaks verification | No | No |
| **Audit trail for policy changes** | Yes: every policy update is an RSL entry | No explicit audit trail beyond git history | No explicit audit trail beyond git history |

---

## System Agnosticism and Backwards Compatibility

This is the ability for the tool to work with any existing Git repository and
any standard Git tooling, without requiring changes to developer workflows.

| | gittuf | Guix | sequoia-git |
|---|---|---|---|
| **Works with existing Git repositories** | Partial: requires policy initialization before use; metadata stored as native Git objects | Partial: requires adding `.guix-authorizations` and a `keyring` branch to the repository | Partial: requires adding `openpgp-policy.toml` and certificate files to the repository |
| **Compatible with popular Git forges** | Yes: SCP-agnostic; optional GitHub app integration for recording PR attestations | Yes: compatible with standard Git forges; no native integration or forge-aware features | Yes: compatible with standard Git forges; no native integration or forge-aware features |
| **Enforcement at the forge level** | Yes: via Configuration A/C in GAP-2; forge can reject non-compliant pushes | No: verification is client-side or CI-based | No: verification is client-side or CI-based |
| **No required changes to developer commit workflow** | Partial: Git-only users need no changes, but gittuf users must sign commits and record RSL entries | No: all commits must be OpenPGP-signed | No: all commits must be OpenPGP-signed |
| **Recovery from policy violations** | Yes: gittuf provides a recovery workflow for unauthorized changes already pushed | Manual recovery required | Manual recovery required |

---

## Summary

All three systems share the baseline configuration that authentication
information is stored in the repository itself, which makes verification
independent of any forge or third-party authority. The key differences however
lie in scope and trust model:

**Guix** optimizes for simplicity and auditability within a project that already
uses OpenPGP universally, though it offers no support for other signing
mechanisms such as SSH keys or Sigstore.
It is authorization invariant, which means that a commit is authentic if and
only if it is signed by a key listed in the `.guix-authorizations` of its parent
makes the trust model transparent and auditable. The tradeoff is that any single
authorized committer can update the authorization list, and there is no
append-only activity log.

**sequoia-git** adds role-based authorization on top of commit signing, allowing
a policy to specify which signers are authorized to make which types of changes
(commits, releases, policy updates) making it more expressive than Guix's flat
key list but it still requires unanimous single-party authorization for policy
changes and relies on standard git history for its audit trail.

**gittuf** addresses a broader set of goals: threshold-based authorization for
both content changes and policy updates, granular path-based delegation, an
independent append-only activity log, support for multiple signing backends
including keyless Sigstore, and optional forge integration.

---
