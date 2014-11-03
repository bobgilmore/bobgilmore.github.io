---
layout: post
title: Changing Your Rails Project Database
tags:
- rails
---
I usually prefer PostgreSQL to SQLite, so I keep a `-d postgres` in my `~/.railsrc` file.  (Actually, it's an alias to another file, but that's a story for another day.)

But last week, I was in a training session at [DockYard](http://dockyard.com/) (thanks, [Brian!](https://twitter.com/bcardarella)), and we were creating a new Rails app as a small part of a larger demo.  We created the app, made a *bunch* of tweaks, and then tried to run it.

Wait - `role "Foo" does not exist`?   What the...?  Oh, Hell, right, Postgres.  Gotta go in to the DB, create the role, reassign the password, oh, man, wait, this is a one-off demo.  How do I switch this app to just use SQLite instead...?

Turns out that you only have to tweak two files to move from Postgres to SQLite or vice versa.  Here, I describe the PostgreSQL to
SQLite conversion.  Reverse as needed.

## `Gemfile`
Replace


~~~~~
# Use postgresql as the database for Active Record
gem 'pg'
~~~~~

with

~~~~
# Use sqlite3 as the database for Active Record
gem 'sqlite3'
~~~~
and run `bundle`.

## `config/database.yml`

Ignore  the comments relating to the drivers.

Then, in each of the sections (development, test, production)...

- Change the `adapter` from `postgresql` to `sqlite3`
- Change the `database` from `ProjectName_development` (or test or production...) to `db/development.sqlite3` (ditto)
- Remove the `encoding: unicode` from each section
- Remove the `username: ProjectName` from each section
- Remove the `password: ` line (that contains no password) from each section
- Add a `timeout: 5000` line to each section

Then rerun the appropriate `rake:db` commands to re-initialize the new database, and you're done!  Enjoy.