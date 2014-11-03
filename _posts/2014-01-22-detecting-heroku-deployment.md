---
title: Detecting that You're Deployed to Heroku
tags:
- heroku
- ruby
date: 2014-01-22 8:00:00
layout: post
---
How do you detect that you're deployed to Heroku, so you can make your code run differently when deployed?  **You don't**.  Instead, you look to see if a particular *behavior* has been requested, and act accordingly.

For some contract work we integrated [Bugsnag](https://bugsnag.com/) into a Rails project.  Even though we only had Bugsnag turned on in Rails production mode, we would always throw a few errors during our final local "production" testing, cluttering up the logs and [HipChat](https://www.hipchat.com/).

To turn off Bugsnag when working locally, I wanted to figure out how to detect when we were being served from Heroku.  I finally figured out that that's *not* what I wanted; I wanted to know that I was running in an environment that *required* Bugsnag integration.  That's deployment-platform-agnostic, so I shouldn't *really* be looking to see if I'm on Heroku or not!

## Environment Variables for Toggling Capabilities ##

We decided to go with:

> Choose a new environment variable.  If it's nonexistent or "falsy" (false, or 0, or whatever) behave "like a developer machine." If it exists, with a "truthy" value, behave "like you're really deployed."

That way, when a new developer joins the team, he or she will get the "local developer behavior" "for free."  You have to tweak your installation a bit to work like "true deployment."

In our case, we used the environment variable "REPORT_EXCEPTIONS."  We set it to 'true' in the Heroku shell, like this...

    heroku config:set REPORT_EXCEPTIONS=true

... and left it nonexistent on our development machines.  See the [Heroku configuration vars page](https://devcenter.heroku.com/articles/config-vars).  (Today, I would probably use [Foreman](http://blog.daviddollar.org/2011/05/06/introducing-foreman.html) and heroku-config.  Again, see the [configuration vars page](https://devcenter.heroku.com/articles/config-vars).)

Then, in the code, act on that environment variable, **or lack thereof.**

{% highlight ruby %}
if ENV['REPORT_EXCEPTIONS'] == 'true'
  configure_for_error_reporting
end
{% endhighlight %}

