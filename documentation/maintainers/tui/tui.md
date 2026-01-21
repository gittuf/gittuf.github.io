---
title: The gittuf TUI
parent: 4. gittuf for Maintainers
layout: default
nav_order: 5
permalink: /documentation/maintainers/tui
---

# The gittuf TUI

{: .experimental}

> We're working on improving the gittuf TUI, as it's a complex piece of code. If
> you encounter any issues with the TUI, we ask that you [report them] to us so
> that we can improve it. 

So far, we've seen how we can edit gittuf metadata with commands, with one
command reflecting a singular operation in gittuf metadata. This can quickly
become cumbersome for repositories where frequent updates are needed or with
complex policies.

gittuf provides an alternative UI for managing gittuf metadata, called the
Terminal UI (TUI). It's a GUI, just rendered in your terminal window instead as
a discrete application window.

The gittuf TUI is navigated as any other terminal UI, using your arrow keys to
select an operation from the menu and the appropriate fields and buttons.

The TUI is capable of managing all parts of gittuf metadata. As such, after you
perform the initial repository initialization procedure with commands, we
envision that you will need only interact with the TUI (unless you prefer the
CLI).

To invoke the gittuf TUI, run:

```
gittuf policy tui [-k your signing key]
```

Specifying a siging key is only required if you wish to make changes to gittuf
metadata, and is not required for operations that only _view_ gittuf metadata.

TODO: Expand.

[report them]: https://github.com/gittuf/gittuf/issues/new
