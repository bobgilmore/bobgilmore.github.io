---
layout: post
title: Bad Quote Glyphs? Think Encoding.
tags:
- html
- jekyll
---
If you're seeing bad glyphs for quotes, ellipses, etc., think "encoding?"

Ever since I started, I've been struggling with quotes; single quotes (or "inverted commas"), double quotes, and ellipses kept rendering the wrong glyphs, such as the Euro sign.  I wasted a lot of time trying to tell the HTML renderers how to handle these correctly, all the while wondering why I wasn't seeing *everyone* complain about it!

It's simple; I forgot to specify the correct encoding in my templates.  Argh!  This has bitten me before.

Changing my template header from *this*...

    {% highlight html %}
    <html>
      <head>
    {% endhighlight %}

...to this...

    {% highlight html %}
    <!doctype html>
    <html xml:lang="en" lang="en">
      <head>
    {% endhighlight %}

fixed the problem.

Yes, the header needs work, but encoding issue, the bane of my existence, is solved!