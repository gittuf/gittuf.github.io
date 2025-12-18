---
title: Managing Rules
parent: Policy
layout: default
nav_order: 2
permalink: /documentation/maintainers/policy/rules
---

# Managing Rules

Rules in gittuf policy are the powerful building block of your policy. They
allow you to define the behavior allowed on your repository, and can target
changes made at a commit level, or changes at a file level.

## The Default-Allow Rule

By default, gittuf does not restrict changes to any branch or file. This is
because of the **default-allow** rule present in gittuf. This rule is not
removable, and is intended to fail-open so that the entire Git repository does
not become suddenly restricted after simply applying gittuf.

Whenever a rule is applied to a certain part of the repository, gittuf will then
treat any operation not allowed in the rule as invalid, turning into a
**default-deny** system _for that part of the repository only_.

In short, nothing is protected at the start, and as soon as something is
protected, only those users authorized to make changes to the protected part are
allowed to do so.

## Branch Protection Rules

gittuf supports rules protecting two types of activity in a Git repository. The
first is a **branch protection rule**, which authorizes the specified users to
make commits to the branch in question.

This type of rule is indicated by the `git:` prefix in its pattern, e.g.:

```
git:refs/heads/main
```

The above snippet would mean the rule protects the `main` branch of the Git
repository.

## File Protection Rules

The other type of rule gittuf supports is a **file protection rule**, which
allows the specified users to edit the specified files.

This type of rule is indicated by the `file:` prefix in its pattern, e.g.:

```
file:README.md
```

The above snippet would mean the rule protects the file `README.md` in any
branch of the Git repository.

## Defining a Rule

Now that we know the types of rules we can make, let's see how we can define
some in gittuf. Each rule contains the following information:

- The rule name
- The namespaces which the rule is to apply to
- The users authorized to make changes to these protected namespaces
- The threshold of users required to approve any single change to the protected
  namespace

To add a rule, run the `gittuf policy add-rule` command:

```
gittuf policy add-rule -k <your signing key>
                       --rule-name <name>
                       --rule-pattern <pattern>
                       --authorize <principals>
```

If you want to protect the `main` branch of the repository, and require that both
Alice and Bob must approve any change to the branch, the command would look like:

```
gittuf policy add-rule -k <your signing key>
                       --rule-name protect-main
                       --rule-pattern git:refs/heads/main
                       --authorize Alice
                       --authorize Bob
                       --threshold 2
```

## Next: gittuf Across Multiple Repositories

Now that we've seen how gittuf policies work, let's take a look at a bigger
picture: how [gittuf policies can span multiple repositories].

[gittuf policies can span multiple repositories]: /documentation/maintainers/multirepo
