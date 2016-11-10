Heroku buildpack: Mojo
======================

This is a Heroku buildpack that runs Mojolicious based web applications using Daemon.

Based on: miyagawa/heroku-buildpack-perl

Usage
-----

Example usage:

    $ ls
    cpanfile
    app.psgi
    lib/

    $ cat cpanfile
    requires 'Plack', '1.0000';
    requires 'DBI', '1.6';

    $ heroku create --stack cedar-14 --buildpack https://github.com/juliodcs/heroku-buildpack-mojo.git

    $ git push heroku master
    ...
    -----> Heroku receiving push
    -----> Fetching custom buildpack
    -----> Perl/Mojolicious app detected
    -----> Installing dependencies

The buildpack will detect that your app has an `app.pl` in the root.

Libraries
---------

Dependencies can be declared using `cpanfile` (recommended) or more traditional `Makefile.PL`, `Build.PL` and `META.json` (whichever you can install with `cpanm --installdeps`), and the buildpack will install these dependencies using [cpanm](http://cpanmin.us) into `./local` directory.

