---
layout: post
title: Deferring Jekyll Post Publication
tags:
- blogging
- jekyll
- yaml
date: 2014-01-13 08:00:00
---
Jekyll posts are automatically generated from the Markdown (or Textile) files in the \_posts directory.  But you can defer publication (really, deferring .html file generation into the _site directory) of particular files until a certain date or time.  I think the doc on this is a little scattered, so I'll go over what I've found here...

## Only Properly Named _posts are Considered ##

In order to be published, a file...

1. Must be in the _posts directory, and 
2. Must have a name of the form `YYYY-MM-DD-brief-description.md` (or other extensions as applicable.  I'm going to ignore those from now on.)  The `YYYY-MM-DD` specifier must be valid (i.e., numbers); `2014-01-XX-my-draft-file.md` will *not* be published. 

If it doesn't meet those two critera, it won't be published.  Period, end of story.

## Every Jekyll Post has a Date ##

`_posts` in Jekyll files can specify their "date" in one of two ways:

1. As a `date` entry in the YAML "front-matter" (a section of YAML data contained at the very top of the file, see [Jekyll's YAML front-matter documentation](http://jekyllrb.com/docs/frontmatter/), or
2.  Embedded within the file name itself, as we saw above.

Now, a post *must* have a valid date embedded within its name since, as we saw above, Jekyll won't even *look* at a file without one.  But, once it's "decided to look," **the date (if any) in the YAML front-matter always trumps the date in the file name.**

So, for example, if `2014-01-07-sales-meeting.md` contains the following YAML front-matter:

~~~~
title: Sales Meeting Results
date: 2014-02-23 10:30
~~~~

, the date of the post is February 23rd t 10:30 AM, *not* January 7th.

## Deferring Posts ##

By default, *all* "valid" (see "Only Properly Named \_posts are Considered", above) posts are published.  If you want to prevent "future posts" from being published, then in the Jekyll installation's `_config.yml` file add:

 `future: false`

That makes the generator look at the *date* of each post (see "Every Jekyll Post has a Date").  Posts whose date is in the future will not be published.

To handle the time properly, I recommend also setting the timezone in `_config.yml` to avoid server time zone issues.  For example, I have 

       timezone: America/New_York
in my config file.

So, you can "queue up" future posts in your _posts directory by giving them YAML front-matter dates in the future.

## Not an Auto-Poster ##

This does *not* mean that, when you finally hit the date of a future post, the post will automatically appear.  It only means that it will appear *the next time you publish!*  You'll need some other way to "tickle" Jekyll, or your Heroku build pack, or whatever, to do the publishing.  I have some ways to do that that I'll describe soon.