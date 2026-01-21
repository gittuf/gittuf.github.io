---
title: 4. gittuf for Maintainers
parent: Documentation
layout: default
nav_order: 4
permalink: /documentation/maintainers
---

# Part 4: gittuf for Maintainers

gittuf is capable of enforcing write access control policies on Git
repositories, without the need for a centralized platform to enforce said
policies. Because of this, you must use the gittuf tool to define your desired
policy for your Git repository, similar to how you use Git.

As with any security policy, designing an effective policy can be challenging
task. This guide is intended to help you understand how gittuf works, so that
you can build and apply your policy.

## A Note on Signing Keys

Before you begin setting up gittuf, please ensure you have read [Signing Keys]
in Part 3, gittuf for Contributors, for information on how signing keys are
treated in gittuf.

## Reading this Guide

The administration documentation for gittuf is divided into five parts, with
each section taking you through how each part of gittuf metadata is initialized
and managed.

While you need not read it in order if you are only interested in a specific
part, we suggest reading through [Trust Architecture] first so you understand
how gittuf structures trust and user permissions, as well as definitions used in
this section.

## Next: Trust Architecture

Let's take a quick look at how gittuf handles trust in [Trust Architecture].

[Signing Keys]: /documentation/contributors/signing-keys
[Trust Architecture]: /documentation/maintainers/design
