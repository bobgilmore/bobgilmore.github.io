---
title: Fixing Twitter DMs on iOS
tags:
- ios
- twitter
date: 2014-04-28 10:00:00
layout: post
---

I love [Twitterrific for iOS](http://twitterrific.com/ios), but I'm DMing more and more these days, and Twitterrific just wasn't supporting DMs.  So I switched to the official Twitter app.  Hate it!

Finally looked into the Twitterrific problems.  Turns out that when iOS grants credentials to a Twitter client, it *doesn't* grant enough credentials for DMs.

To fix it; *don't* rely on iOS's built-in Twitter integration.  Go into your favorite Twitter app, delete your account, and log in to that app again *"by hand,"* going through the web page-based OAuth process.  Problem solved, DMs appear again!  Thanks Iconfactory!
