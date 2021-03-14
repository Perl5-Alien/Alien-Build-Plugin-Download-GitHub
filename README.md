# Alien::Build::Plugin::Download::GitHub ![linux](https://github.com/PerlAlien/Alien-Build-Plugin-Download-GitHub/workflows/linux/badge.svg)

Alien::Build plugin to download from GitHub

# SYNOPSIS

```perl
use alienfile;

...

share {

  plugin 'Download::GitHub' => (
    github_user => 'PerlAlien',
    github_repo => 'dontpanic',
  );

};
```

# DESCRIPTION

This plugin will download releases from GitHub.  It is generally preferred over
[Alien::Build::Plugin::Download::Git](https://metacpan.org/pod/Alien::Build::Plugin::Download::Git) for packages that are released on GitHub,
as it has much fewer dependencies and is more reliable.

# PROPERTIES

## github\_user

The GitHub user or org that owns the repository.  This property is required.

## github\_repo

The GitHub repository name.  This property is required.

## include\_assets

Defaulting to false, this option designates whether to include the assets of
releases in the list of candidates for download. This should be one of three
types of values:

- true value

    The full list of assets will be included in the list of candidates.

- false value

    No assets will be included in the list of candidates.

- regular expression

    If a regular expression is provided, this will include assets that match by
    name.

## tags\_only

Boolean value for those repositories that do not upgrade their tags to releases.
There are two different endpoints. One for
[releases](https://developer.github.com/v3/repos/releases/#list-releases-for-a-repository)
and one for simple [tags](https://developer.github.com/v3/repos/#list-tags). The
default is to interrogate the former for downloads. Passing a true value for
["tags\_only"](#tags_only) interrogates the latter for downloads.

## version

Regular expression that can be used to extract a version from a GitHub tag.  The
default ( `qr/^v?(.*)$/` ) is reasonable for many GitHub repositories.

## prefer

How to sort candidates for selection.  This should be one of three types of values:

- code reference

    This will be used as the prefer hook.

- true value (not code reference)

    Use [Alien::Build::Plugin::Prefer::SortVersions](https://metacpan.org/pod/Alien::Build::Plugin::Prefer::SortVersions).

- false value

    Don't set any preference at all.  The order returned from GitHub will be used if
    no other prefer plugins are specified.  This may be reasonable for at least some
    GitHub repositories.  This is the default.

# CAVEATS

The GitHub API is rate limited.  The unauthenticated API is especially so.  This may
render this plugin inoperative for a short time after only a little testing.  Please see

[https://github.com/PerlAlien/Alien-Build-Plugin-Download-GitHub/issues/3](https://github.com/PerlAlien/Alien-Build-Plugin-Download-GitHub/issues/3)

# AUTHOR

Author: Graham Ollis <plicease@cpan.org>

Contributors:

Roy Storey (KIWIROY)

# COPYRIGHT AND LICENSE

This software is copyright (c) 2019 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
