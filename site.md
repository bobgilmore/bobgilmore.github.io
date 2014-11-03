---
title: About the Site
layout: default_layout
change_frequency: daily
priority: 1.0
---

About the Site
=====
The main implementation is a [Jekyll](http://github.com/mojombo/jekyll/) app running on an [Heroku](https://www.heroku.com) instance.

Workflow
----

1. I commit blog entries and other pages in [Markdown](http://daringfireball.net/projects/markdown/), which is automatically translated into HTML by Jekyll.
2. I push the entries (just the Markdown) into a public [Github repo](https://github.com/bobgilmore/jekyll-blog).
3. When I'm ready to update the blog proper, I push again, this time to my Heroku.

Technologies
-----

Jekyll is "pure" Ruby, not Rails, so there's no builtin asset pipeline.  I added one with the [jekyll-assets](https://github.com/ixti/jekyll-assets) gem.  That lets me use [Sass](http://sass-lang.com/) rather than plain old (ugh) CSS.

[kramdown](http://kramdown.gettalong.org/) (one of Jekyll's alternative HTML translators) replaces Jekyll's default, [Maruku](http://maruku.rubyforge.org/).

[jQuery](http://jquery.com/) is the indispensable JavaScript library.

[Thoughtbot's](http://thoughtbot.com) libraries [Bourbon](http://bourbon.io/) and [Neat](http://neat.bourbon.io/) provide responsive layout.

Default CSS provided by Thoughtbot's [Bitters](https://github.com/thoughtbot/bitters) because Bourbon, Neat *needs* a dash of Bitters.

The RSS feed is served directly from within Heroku (no need for FeedBurner etc. yet) via `feed.xml` from [snaptortise's Jekyll RSS Feed Templates](https://github.com/snaptortoise/jekyll-rss-feeds).

Log management on the Heroku end handled by [Logentries](https://addons.heroku.com/logentries).

Comments handled by [Disqus](http://disqus.com/).

I *considered* migrating off of [Pygments](http://pygments.org/) (for code syntax highlighting) to [CodeRay](http://coderay.rubychan.de/), but the latter doesn't highlight SCSS yet, so I'm sticking with the former.
