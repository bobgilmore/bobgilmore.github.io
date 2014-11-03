---
title: Rails Upgrades and Migrations 
tags:
- rails
date: 2014-08-06 08:00:00
layout: post
---

When upgrading Rails, be sure to run `rake db:migrate` *even if you aren't committing a migration.* See if your `schema.rb` changed.  If it did, understand why, then commit the change along with the rest of the upgrade.

I was surprised by new `limit` calls in my schema.  Turns out that Rails 4.1.2 added information to the schema to ensure that MySQL `float`s and `doubles` are handled properly.  Since we didn't migrate for the upgrade job, they mysteriously appeared on the next migration.