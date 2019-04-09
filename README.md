# Alien::Build::Plugin::Download::GitHub [![Build Status](https://secure.travis-ci.org/Perl5-Alien/Alien-Build-Plugin-Download-GitHub.png)](http://travis-ci.org/Perl5-Alien/Alien-Build-Plugin-Download-GitHub)

Alien::Build plugin to download from GitHub

# SYNOPSIS

    use alienfile;

    ...

    share {
    
      plugin 'Download::GitHub' => (
        github_user => 'Perl5-Alien',
        github_repo => 'dontpanic',
      );
    
    };

# DESCRIPTION

This plugin will download releases from GitHub.  It is generally preferred over
[Alien::Build::Plugin::Download::Git](https://metacpan.org/pod/Alien::Build::Plugin::Download::Git) for packages that are released on GitHub,
as it has much fewer dependencies and is more reliable.

# PROPERTIES

## github\_user

The GitHub user or org that owns the repository.  This property is required.

## github\_repo

The GitHub repository name.  This property is required.

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

[https://github.com/Perl5-Alien/Alien-Build-Plugin-Download-GitHub/issues/3](https://github.com/Perl5-Alien/Alien-Build-Plugin-Download-GitHub/issues/3)

# AUTHOR

Author: Graham Ollis <plicease@cpan.org>

# COPYRIGHT AND LICENSE

This software is copyright (c) 2019 by Graham Ollis.

This is free software; you can redistribute it and/or modify it under
the same terms as the Perl 5 programming language system itself.
