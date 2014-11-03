---
title: Serving (One-Off) Files Securely on Heroku
tags:
- heroku
- ssl
date: 2014-01-24 8:00:00
layout: post
---
If you need to serve a file or two from your Heroku-based site with SSL, but don't need to serve the whole thing that way, there's an easy way to do it that piggybacks off of Heroku's certificate.  See [Heroku's SSL Endpoint documentation](https://devcenter.heroku.com/articles/ssl-endpoint) for directions.

My Problem
------
A few days ago I posted about [using Gistdeck](/2014/01/20/gistdeck.html), with instructions for modified version.  Just before I released them, I found that using my version of Gistdeck on a real Gist caused horrible Chrome warnings about site security.  That's because GitHub serves Gists via HTTP**S**, but my site was serving Gistdeck via plain old HTTP.  So when I used the bookmarklet, I was loading non-secure data into a secure page.  Boom, warnings galore!

Fortunately, I didn't have to get my own certificate just to serve those two files (one JS, one CSS).  Heroku lets me use their certificate, with one catch.  It's not really a "catch" so much as a "fact of life"...

Use Your "Real" Heroku App Address
------
Of course (it's obvious), you can't use Heroku's certificate for your own domain!  Try to serve something in the `bobgilmore.name` domain using Heroku's SSL certificate.  That's saying "trust me, it *looks* like Heroku is serving it, but this bobgilmore guy *really* is.  You totally believe that, right?"

To deal with it, use your Heroku app's "real" app name when serving via HTTPS.  So, while most of this blog is served from [http://blog.bobgilmore.name](http://blog.bobgilmore.name), the Gistdeck code is served, *securely*, from [https://bobgilmore-blog.herokuapp.com/gistdeck/gistdeck.js](https://bobgilmore-blog.herokuapp.com/gistdeck/gistdeck.js).

Obviously you wouldn't want to serve a *lot* of code this way, but for the occasional file or two it's fine.  As long as you don't get into any cross-site scripting issues...