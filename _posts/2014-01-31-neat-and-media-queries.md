---
title: Neat and Media Queries
tags:
- bourbon
- css
- neat
date: 2014-01-31 10:00:00
layout: post
---
Last month I mentioned that [I love the semantic grid framework in Neat](/2013/11/14/blog-tech-5.html), but didn't go into a lot of detail.  Here's an example of what's so great about it...

Changing Grid Columns for Mobile
--------
Things may change by the time you read this, but right now this blog has a 2-empty-column left rail, an 8-column content region, and a 2-empty-column right rail by "default."  The CSS looks like this:

    {% highlight scss %}
    .left-rail     { @include span-columns(2); }
    .center-rail   { @include span-columns(8); }
    .right-rail    { @include span-columns(2); @include omega(); }
    {% endhighlight %}

That looks pretty good in a desktop layout, but in a really narrow page (like an iPhone in portrait mode), that's just too much whitespace on the sides!  

To fix it just detect the configuration via a [media query](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Media_queries) and write the "obvious" code; hide the left and right rails, and let the center rail consume all 12 columns of the Neat layout.

    {% highlight scss %}
    @media only screen and (orientation: portrait) {
      .left-rail,.right-rail { display: none; }
      .center-rail { @include span-columns(12); }
    }
    {% endhighlight %}

See what happened there?  Since Neat lets me specify **in the CSS** how many columns a class consumes, I simply `@include` the new column count.  I'll admit, I don't remember how to pull that off in Bootstrap, but I'm pretty sure that it isn't *that* easy!

If anyone wants to include the Bootstrap code in a comment, go for it!