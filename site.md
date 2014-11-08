---
title: About the Site
layout: default_layout
change_frequency: daily
priority: 1.0
---

About the Site
=====
The main implementation is a [Jekyll](http://github.com/mojombo/jekyll/) app. Powered by, and served from, [GitHub Pages](https://pages.github.com/).

Workflow
----

1. I commit blog entries and other pages in [Markdown](http://daringfireball.net/projects/markdown/), which is automatically translated into HTML by Jekyll.
2. I push the entries (just the Markdown) to a particular [Github repo](https://github.com/bobgilmore/bobgilmore.github.io).
3. GitHub runs the Jekyll engine for me, generating HTML from the Markdown.

I used to run a Jekyll instance on [Heroku](https://www.heroku.com/), but got tired of updating Jekyll myself, so I decided to let GitHub manage it.

Technologies
-----

Jekyll is "pure" Ruby, not Rails, so there's no builtin asset pipeline.  Fortunately, GitHub maanges that from me, generating [Sass](http://sass-lang.com/) as necessary.  (When I was hosting on Heroku, I added an asset pipeline with the [jekyll-assets](https://github.com/ixti/jekyll-assets) gem.)

[kramdown](http://kramdown.gettalong.org/) (one of Jekyll's alternative HTML translators) replaces Jekyll's default, [Maruku](http://maruku.rubyforge.org/).

[jQuery](http://jquery.com/) is the indispensable JavaScript library.

[Thoughtbot's](http://thoughtbot.com) libraries [Bourbon](http://bourbon.io/) and [Neat](http://neat.bourbon.io/) provide responsive layout.

Default CSS provided by Thoughtbot's [Bitters](https://github.com/thoughtbot/bitters) because Bourbon, Neat *needs* a dash of Bitters.

The RSS feed is served directly from within GitHub (no need for FeedBurner etc. yet) via `feed.xml` from [snaptortise's Jekyll RSS Feed Templates](https://github.com/snaptortoise/jekyll-rss-feeds).

(When I was hosted on Heroku, log management was handled by [Logentries](https://addons.heroku.com/logentries).  GitHub error messages are pretty sparse; I need to find a replacement.)

Comments handled by [Disqus](http://disqus.com/).

I *considered* migrating off of [Pygments](http://pygments.org/) (for code syntax highlighting) to [CodeRay](http://coderay.rubychan.de/), but the latter doesn't highlight SCSS yet, so I'm sticking with the former.
