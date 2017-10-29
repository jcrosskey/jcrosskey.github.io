---
layout: post
title:  "Git pre-push hook"
categories: git, hook
---
**pre-push** hook is run after `git push` command updates the remote ref, and before the real push happens. It can be used to check what is to be pushed, and abort the operation if necessary. There are some caveats to using this hook, which I will describe in this post.

### [From the documentation][git-doc]
The hook is called with two parameters which provide the name and
location of the destination remote, if a named remote is not being used both
values will be the same.

Information about **what is to be pushed** is provided on the hook's standard
input with lines of the form:

```
  <local ref> SP <local sha1> SP <remote ref> SP <remote sha1> LF
```

For instance, if the command +git push origin master:foreign+ were run the
hook would receive a line like the following:

```
  refs/heads/master 67890 refs/heads/foreign 12345
```

although the full, 40-character SHA-1s would be supplied.  If the foreign ref
does not yet exist the `<remote SHA-1>` will be 40 `0`.  If a ref is to be
deleted, the `<local ref>` will be supplied as `(delete)` and the `<local
SHA-1>` will be 40 `0`.  If the local commit was specified by something other
than a name which could be expanded (such as `HEAD~`, or a SHA-1) it will be
supplied as it was originally given.

If this hook exits with a non-zero status, 'git push' will abort without
pushing anything.  Information about why the push is rejected may be sent
to the user by writing to standard error.

### Arguments

### Input from stdin

### References
1. [git documentation on pre-push hook][git-doc]

[git-doc]:https://git-scm.com/docs/githooks#_pre_push

