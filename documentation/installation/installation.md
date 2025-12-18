---
title: 2. Installation
parent: Documentation
layout: default
nav_order: 2
permalink: /documentation/installation
has_toc: no
---

# Part 2: Installing gittuf

gittuf is written in [Go], which makes it easy to install. We recommend
installing gittuf using pre-built binaries from package managers or from GitHub
itself, as it's the easiest way to get started. If you prefer building from
source, see the [building from source] instructions.

## Package Managers

### Windows

gittuf is available on [Winget], which is pre-installed on Windows 11 and above:

```
winget install gittuf.gittuf
winget install gittuf.git-remote-gittuf
```

Proceed to the [next steps below].

### macOS

gittuf is available on [Homebrew]. Once Homebrew is installed, run:

```
brew install gittuf
```

Proceed to the [next steps below].


### Linux

gittuf is packaged with a lot of Linux package managers, but these versions tend
to be out of date. We therefore recommend installing gittuf from pre-built
binaries (see below), or [building from source] source on Linux.

If you prefer to use your package manager, please check the version of gittuf
offered so that you're running the latest version:

[![Packaging status](https://repology.org/badge/vertical-allrepos/gittuf.svg)](https://repology.org/project/gittuf/versions)

Proceed to the [next steps below].

### FreeBSD

gittuf is not (yet) packaged with `pkg` on FreeBSD systems. See below for
installing gittuf from pre-built binaries, or see the [building from source]
documentation.

## Manual Installation from Pre-built Binaries

gittuf's binaries are portable, and do not require any special installation
steps beforehand.

To download the binaries, see the [GitHub releases] page for gittuf, and pick
the latest release. There are two binaries to download:

- The main `gittuf` binary, and,
- The `git-remote-gittuf` binary, which automatically manages day-to-day gittuf
  operations

After you have downloaded the binaries, place them somewhere in your `$PATH`, and
proceed to the [next steps below].

### (Optional) Verify with Cosign

[Cosign] is used to sign gittuf's binaries, and ensure that you are receiving
authentic code. You do not need to verify with Cosign to use these binaries, but
you may do so if you wish.

To verify using Cosign, make sure that you have installed it, and then follow
the instructions for your OS. After you verify, proceed to the [next steps
below].

#### Unix-like Systems

The following bash script will download the gittuf binaries, and verify them with
Cosign:

```sh
# Modify these values as necessary.
# One of: amd64, arm64
ARCH=amd64
# One of: linux, darwin, freebsd
OS=linux
# See https://github.com/gittuf/gittuf/releases for the latest version
VERSION=0.12.0
cd $(mktemp -d)

curl -LO https://github.com/gittuf/gittuf/releases/download/v${VERSION}/gittuf_${VERSION}_${OS}_${ARCH}
curl -LO https://github.com/gittuf/gittuf/releases/download/v${VERSION}/gittuf_${VERSION}_${OS}_${ARCH}.sig
curl -LO https://github.com/gittuf/gittuf/releases/download/v${VERSION}/gittuf_${VERSION}_${OS}_${ARCH}.pem

cosign verify-blob \
    --certificate gittuf_${VERSION}_${OS}_${ARCH}.pem \
    --signature gittuf_${VERSION}_${OS}_${ARCH}.sig \
    --certificate-identity https://github.com/gittuf/gittuf/.github/workflows/release.yml@refs/tags/v${VERSION} \
    --certificate-oidc-issuer https://token.actions.githubusercontent.com \
    gittuf_${VERSION}_${OS}_${ARCH}

sudo install gittuf_${VERSION}_${OS}_${ARCH} /usr/local/bin/gittuf
cd -
gittuf version
```

#### Windows

Copy and paste these commands in PowerShell to install gittuf. Please remember
to change the version number (0.12.0 in this example) and architecture (amd64 in
this example) according to your use-case and system.

```powershell
curl "https://github.com/gittuf/gittuf/releases/download/v0.12.0/gittuf_0.12.0_windows_amd64.exe" -O "gittuf_0.12.0_windows_amd64.exe"
curl "https://github.com/gittuf/gittuf/releases/download/v0.12.0/gittuf_0.12.0_windows_amd64.exe.sig" -O "gittuf_0.12.0_windows_amd64.exe.sig"
curl "https://github.com/gittuf/gittuf/releases/download/v0.12.0/gittuf_0.12.0_windows_amd64.exe.pem" -O "gittuf_0.12.0_windows_amd64.exe.pem"

cosign verify-blob --certificate gittuf_0.12.0_windows_amd64.exe.pem --signature gittuf_0.12.0_windows_amd64.exe.sig --certificate-identity https://github.com/gittuf/gittuf/.github/workflows/release.yml@refs/tags/v0.12.0 --certificate-oidc-issuer https://token.actions.githubusercontent.com gittuf_0.12.0_windows_amd64.exe
```

## Next: Using and Administering gittuf

Next, now that gittuf has been installed, let's see how gittuf is used
day-to-day with [Part 3: Using gittuf].

[Go]: https://go.dev
[building from source]: /installation/source/
[Winget]: https://learn.microsoft.com/en-us/windows/package-manager/winget
[Homebrew]: https://brew.sh
[GitHub releases]: https://github.com/gittuf/gittuf/releases
[Cosign]: https://docs.sigstore.dev/cosign
[Part 3: Using gittuf]: /documentation/using
[next steps below]: #next-using-and-administering-gittuf
