---
title: Trim the Fastlane Snapfile for Debugging
tags:
- fastlane
- ios
date: 2018-09-18 22:30:00
layout: post
---
# Trim the Fastlane Snapfile for Debugging
The default `Snapfile` that `fastlane init` creates for you is fine, with one exception.

Once you have your UI test files written, complete with `snapshot()` calls, you run

`fastlane snapshot`

at the shell to generate the screenshots. But the debug cycle is way too long - it takes _forever_ to finish and show you what’s wrong. That’s because the default `Snapfile` runs a _bunch_ of Simulators.

Do yourself a favor and restrict it to run in **one** Simulator during the debugging process.

To do this, I change the default devices list from the completely commented-out (and therefore ineffective) default list

```ruby
# A list of devices you want to take the screenshots from
# devices([
#   "iPhone 8",
#   "iPhone 8 Plus",
#   "iPhone SE",
#   "iPhone X",
#   "iPad Pro (12.9-inch)",
#   "iPad Pro (9.7-inch)",
#   "Apple TV 1080p"
# ])
```

to a single-entry list:

```ruby
# A list of devices you want to take the screenshots from
devices([
  "iPhone 8",
#   "iPhone 8 Plus",
#   "iPhone SE",
#   "iPhone X",
#   "iPad Pro (12.9-inch)",
#   "iPad Pro (9.7-inch)",
#   "Apple TV 1080p"
])
```

Expand it back out to hit all Simulators after you've finished your basic debugging. But when you're debugging, be sure to shrink it back down to one device type.

Similarly, if your "production" `Snapfile` uses multiple languages, trim the language list down while debugging.

* First, trim it down to your development language and get thing working there.
* Then, replace your development language with a *different* supported language, and fix the bugs related to other languages. Trust me, you'll have some.
* Once you're finished, expand back out to the full language list.
