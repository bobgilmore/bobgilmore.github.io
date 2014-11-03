---
layout: post
title: Changing Jekyll's HTML Translator from Maruku to kramdown
tags:
- jekyll
- markdown
---
I replace Maruku with Kramdown.  Why, and How?

Why?
----
Last week I was getting incorrect glyphs in my pages.  I thought that there was a bad setting in the HTML translator.  I dove into the config, and couldn't fix it via translator settings.  Of course, now I know that the bad rendering was caused by <a href='/2013/12/09/bad-quotes-encoding.html'>bad encoding</a>, but I didn't know that then.

While investigating, I found some reports of shortcomings in the Maruku translation engine, and started to think about swapping in a different one.  But which?  Jekyll [supports](https://twitter.com/jekyllrb/status/408631134009163776) Maruku (default), [kramdown](http://kramdown.gettalong.org/), [RedCloth](http://redcloth.org/), and [RDiscount](http://dafoster.net/projects/rdiscount/).

This may be cheating :-) but I pinged the all-knowing Brett Terpstra, to ask *him* which translator he uses.  [He said that he uses kramdown](https://twitter.com/ttscoff/status/408600898844499969).  Let's face it, whichever Markdown translation engine Brett uses is good enough for me!  So kramdown it is.

How?
----
This bit is simple; the Jekyll HTML translator is [set in Jekyll's _config.yml file](http://jekyllrb.com/docs/configuration/). Add the following section, and restart the server / push to Heroku:

    {% highlight yaml %}
    markdown: kramdown
    {% endhighlight %}

See [my _config.yml file](https://github.com/bobgilmore/jekyll-blog/blob/master/_config.yml) for all of my current settings.