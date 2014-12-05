---
title: FactoryGirl and after_initalize
tags:
- rails
- testing
date: 2014-12-05 08:00:00
layout: post
---

I use [FactoryGirl](https://github.com/thoughtbot/factory_girl) for testing, and found a major problem *and* solution last week.

The Problem
-----
We use Rails `after_initialization` [callbacks](http://api.rubyonrails.org/classes/ActiveRecord/Callbacks.html) in object construction, but Rails was acting as if the parameters that we passed to FactoryGirl `build` or `create` calls weren't there.

Well, they weren't, at least not at object initialization..

What's Going On
------
Turns out that FactoryGirl's default behavior is to `new` or `create` the object with *no* arguments, and then set the properties `after` object initialization.  Hey, guess what?  That's too late for use in `after_initialization` callbacks.

Solution
------
Turns out that you can [customize a Factory's constructor](https://github.com/thoughtbot/factory_girl/blob/master/GETTING_STARTED.md#custom-construction) to pass certain (or all) parameters to a particular factory.  I had the best luck using the big hammer of

    initialize_with { new(attributes) }
    
Your results may vary.

Thanks to [@typed](https://twitter.com/typed) for pointing this out!
