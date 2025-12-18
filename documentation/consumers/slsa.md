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

## Source Provenance

TODO.

## Next: gittuf for Contributors

In this part, we saw how gittuf can be used from the consumer perspective to
check that the changes written to a repository are legitimate. We also saw how
gittuf interoperates with the SLSA Source Track.

In the next part, we take a look at [how contributors to a repository use
gittuf].

[#728]: https://github.com/gittuf/gittuf/pull/728
[#1091]: https://github.com/gittuf/gittuf/pull/1091
[SLSA Source Track]: https://slsa.dev/spec/latest/source-requirements
[how contributors to a repository use gittuf]: /documentation/contributors
