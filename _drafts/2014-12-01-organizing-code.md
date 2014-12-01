---
title: Organizing Code Across Macs.
tags:
- git
- productivity
date: 2014-12-01 08:00:00
layout: post
---

I've got a lot of code projects (around 50), and I develop on at least two machines - a Mac Mini at home for "personal" and consulting work, and a Macbook Pro for my primary employer.  I keep things separate, but there's intentional overlap - for example, I use my personal [dotfiles](https://github.com/bobgilmore/dotfiles) and [githooks](https://github.com/bobgilmore/dotfiles) projects at work.  "Toy" projects for exploring new concepts may start on the home machine, but carry over to the laptop for commuting.

Between all those projects for personal, work, and consulting use, I *definitely* need a system to keep track of the code.  Here's what I do.

Code Under Git Control
====
Every bit of code that I write is under `git` management.  Even teeny weenie shell scripts go into a repo so that I can back out ill-advised changes days later.

Shared via GitHub
---
I push most new projects to GitHub to allow sharing between machines.  I have very few private repos - I'm personally paying for only five right now, so my projects go private only when necessary. That's a good discipline to have - the more people see your code, the better.

Once a project is on GitHub, sharing is trivial.  `push` from one machine, `pull` onto another.

... and *Only* via GitHub
------
I know some devs keep their projects in Dropbox so that they're "automagically" shared between projects, no `git push` / `pull` required.  That doesn't work for me - when I have *both* the belt of GitHub *and* the suspenders of Dropbox, I always get sloppy with the `git` commits. So I force myself to rely on `git`.

That said, there *are* bits of my development environment that I synchronize via Dropbox.  For example, my Sublime Text 3 plugins are maintained in Dropbox, so that when I install a plugin on one machine, it's waiting for me on the other.

Kept in a GitHub Organization Hierarchy
===
For awhile I kept all of my repos directly in `$HOME/code`.  That became too unorganized, too fast.

Now, I keep all of my repos in `$HOME/code/organization/projectname`  That makes a *lot* more sense.

- My *personal* projects are directories under `$HOME/code/bobgilmore/`
- *Employer's* projects are directories under `$HOME/code/my_employers_organization/`
- Contract projects are in `$HOME/code/contract_org_1`, `$HOME/code/contract_org_2`, and so on...
- Copies of Thoughtbot repos are in `$HOME/code/thoughtbot`

You get the point.