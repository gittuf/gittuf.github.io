---
title: gittuf and SLSA
parent: 2. gittuf for Consumers
layout: default
nav_order: 2
permalink: /documentation/consumers/slsa
---

# gittuf and SLSA

{: .experimental}

> Support for the features on this page is currently experimental, and is
> dependent on the following PRs: [#728] and [#1091].

gittuf can be used to verify compliance with and generate source provenance for
the [SLSA Source Track]. No special configuration is required from the
repository maintainers to enable this functionality.

## Verification Summary Attestations (VSAs)

gittuf supports writing [Verification Summary Attestations]. VSAs either as a
_bundle of VSAs_, one for each gittuf policy, and a single, _unified VSA_, for
all policies together.

To write a bundle of all VSAs, use the `--write-all-vsas` flag with `gittuf
verify-ref`:

```
gittuf verify-ref --write-all-vsas vsa.bundle
```

To write a unified VSA, use the `--write-unified-vsa` flag instead:

```
gittuf verify-ref --write-unified-vsa vsa.bundle
```

## Source Provenance

gittuf also supports generating source provenance attestations. Use the
`--write-source-provenance` flag:

```
gittuf verify-ref --write-source-provenance provenance.bundle
```

## Signing the Attestations

You may wish to have the VSA or source provenance attestations be signed. To do
so, append the `--sign-source-attestation` flag in conjunction with any of the
above options:

```
gittuf verify-ref --write-[all-vsas, unified-vsa, source-provenance] --sign-source-attestation signing.key
```

## Next: gittuf for Contributors

In this part, we saw how gittuf can be used from the consumer perspective to
check that the changes written to a repository are legitimate. We also saw how
gittuf interoperates with the SLSA Source Track.

In the next part, we take a look at [how contributors to a repository use
gittuf].

[#728]: https://github.com/gittuf/gittuf/pull/728
[#1091]: https://github.com/gittuf/gittuf/pull/1091
[SLSA Source Track]: https://slsa.dev/spec/latest/source-requirements
[Verification Summary Attestations]: https://slsa.dev/spec/v1.2/verification_summary
[how contributors to a repository use gittuf]: /documentation/contributors
