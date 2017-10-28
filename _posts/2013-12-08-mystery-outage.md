---
layout: post
title: Heroku Buildpacks Aren't Specified in Version Control
tags:
- heroku
---
&hellip; and we\'re back from a mystery outage!  Lessons learned&hellip;

Here\'s What we Know
----
While trying to swap HTML translation engines (more on why in a separate post); all Hell broke lose on the site.  Heroku errors whenever attempting to access it.  (I wouldn\'t have known for days that it was broken if I hadn\'t set up [Logentries](https://logentries.com/) on my Heroku site.  Lesson learned; monitor, monitor, monitor.)

It took me a few days in my off-time to fix it, because even reverting *all of the source code* back to its previous state didn\'t fix the problem.  For a few days, the only way that I could make the site work was to revert to an old Heroku slug.  

During the diagnostic process, I upgraded all of the gems.  So, another lesson learned (actually, *refreshed*; I\'ve known this for years, but keep forgetting).  *Don\'t bother to change settings on a library without upgrading it first, or at least **seeing** how out-of-date you. Then, judge accordingly.*

If I\'d sat down for a minute and realized *how* out-of-date some of the libraries in this project were, I would have upgraded seen if *that* fixed the problem.  Oh well, no use crying over spilt milk; I have a site to fix.  Onward&hellip;

Eventually, by looking at the `heroku logs` and by logging in to a `bash` shell in Heroku (`heroku run bash`),  I realized that the Jekyll preprocessor wan\'t running.  After a long, tortuous route, I finally realized that that\'s because the [Jekyll buildpack](https://devcenter.heroku.com/articles/third-party-buildpacks) wasn\'t running.

Are You Kidding Me?
----
But wait, why isn\'t it?  The source code is reverted back to same state it was in day ago, so that means everything should be working as it did back then, right?  Oh My God.  **Heroku Build Packs are controlled by environment settings that AREN\'T  under version control!**

They\'re manipulated by calls to `heroku config`, such as (in this case)  `heroku config:add BUILDPACK_URL= https://github.com/mattmanning/heroku-buildpack-ruby-jekyll`  (BTW, that isn\'t *quite* right, I\'ll talk about why it isn\'t in a follow-up post.)

I don\'t know how I dropped the build pack configuration along the way; I must have done something with `heroku config`  at some point.  But that\'s not the biggest issue, and until about a month ago, I wouldn\'t have realized that it *was* an issue&hellip;

Her's the real problem: *critical configurations, like which Build Packs to use, are not stored under version control!*  

I used to fly by the seat of my pants like that, but recently our DevOps guy has been teaching my new team the value of configuration management.  I get it, I got it, I know it\'s good, but its import never *really* struck home until this side project broke due to bad configuration.  Thanks, Kevin, I get it now!

Going forward, I'm going to document configuration changes like this, either in no-op git commit messages or `Readme.md` files.
