Heroku buildpack: Mojo
======================

This is a Heroku buildpack that runs Mojolicious based web applications using Daemon or Hypertoad.

Heavily based on: miyagawa/heroku-buildpack-perl

All credits to miyagawa.

Usage
-----

Example usage:

    $ ls
    cpanfile
    app-daemon.pl
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

The following app names will be deteced by the buildpack in the root:

    app.pl (starts daemon)
    app-daemon.pl (starts daemon)
    app-hypnotoad.pl (starts hypnotoad)

WARNING: hypnotad needs the app to be preconfigured to listen at port $ENV{PORT}. For example:

    plugin Config => {
        default => {
            hypnotoad => {
                listen => ["http://*:$ENV{PORT}"]
            }
        }
    };

Libraries
---------

Dependencies can be declared using `cpanfile` (recommended) or more traditional `Makefile.PL`, `Build.PL` and `META.json` (whichever you can install with `cpanm --installdeps`), and the buildpack will install these dependencies using [cpanm](http://cpanmin.us) into `./local` directory.

