---
title: Forcing a Jekyll Update on Heroku
tags:
- hazel
- heroku
- ifttt
- jekyll
- siri
date: 2014-01-15 8:00:00
layout: post
---
As I said before, deferring a hosted Jekyll post by specifying a date stamp in the YAML front-matter does *not* mean that the post will magically appear when the timestamp is "satisfied."  You have to "tickle" the host - in my case, Heroku.

## Posts Won't Publish Themselves ##
The only documented way to trigger [the Jekyll buildpack](https://devcenter.heroku.com/articles/third-party-buildpacks) is to push to your Heroku repo.  Of course, at the time that you *want* to publish,

1. You've probably already finished all of your writing awhile (days!) ago, and
2. It's probably the middle of the day, and you're on to other stuff, so you want a "fire and forget" solution that doesn't require a lot of input from you.

## Creating a No-Content Git Commit ##
Turns out that Git supports an almost-no-effort, no-content publish.  `git push` with no committed changes is a no-op.  But **you can create an "empty," pushable commit by running:**

    git commit --allow-empty -m "Commit message"

## Forcing Publication ##
So, my "deferred-posting" workflow is...

1. Push your post into the `_posts` directory, complete with the `date` entry in the YAML front-matter to defer its publication.
2. Some time after publication `date`, do something to create an "empty" commit and push it to Heroku.

## My "Update the Slug" Script ##
I've created a shell script to do the basics of creating an empty commit in a specified git repo and pushing it to Heroku.  I keep it in [my Github dotfiles repo;](https://github.com/bobgilmore/dotfiles) the [script itself is here](https://github.com/bobgilmore/dotfiles/blob/master/scripts/heroku_rebuild_slug.sh).  It probably could be bulletproofed a bit; I'd **love** to get pull requests for improvements!

### Triggering the Script ###

There are a lot of ways to trigger the script; I currently use [an ifttt recipe](https://ifttt.com/recipes/139611) to ultimately force [Hazel](http://www.noodlesoft.com/hazel.php) (on my home Mac server) to run it:

1. I use Siri on iOS to add a Reminder to my Blog reminders list.
2. That Reminder triggers ifttt to drop a particular file, with a particular name, in my Dropbox folder.
3. Hazel detects that file in that location, and triggers the shell script.
4. The shell script creates an empty commit and pushes it to Heroku.
5. Heroku generates a new slug, forcing the Jekyll blog to update itself.

### Other Triggers ###
I'm considering other approaches (mostly based on git pre-commit hooks,) that I'll publish once I have them working.  I'd **love** to hear your approaches to triggering scripts like this!
