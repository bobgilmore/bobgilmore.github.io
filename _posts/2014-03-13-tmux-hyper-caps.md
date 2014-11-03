---
title: tmux, Hyper Key, and Caps Lock
tags:
- tmux
- vim
- unix
- productivity
date: 2014-03-13 10:00:00
layout: post
---

Please, Sir, I want some more (Caps Lock). There are too many awesome keyboard hacks!

Caps Lock as a Hyper Key
----
Months ago, Brett Terpstra's blog showed how to make the [Caps Lock key serve triple-secret overtime](http://brettterpstra.com/2012/12/08/a-useful-caps-lock-key/) as...

1. An Escape key (hello, Vim and Emacs!),
2. A "Hyper Key" (a modifier that *no other app uses for anything*, so *bind the hell out of it* as [Brett describes here](http://brettterpstra.com/2013/01/26/a-guided-tour-of-my-hyper-key-shortcuts/)), *and*
3. An "App Flipper" key to [toggle between two apps](http://brettterpstra.com/2013/01/12/quick-tip-flip-between-two-apps-with-hyper-key/).

.. Or as Ctrl (or Ctrl-A)
----
I just started using tmux for work.  It's mostly for persistent iTerm sessions on an AWS server, but in the back of my mind, I'm thinking about Vim and/or Emacs more and more often (ssshhhh...it's OK, Sublime.  I'll *never* leave you, baby!)

The out-of-the-box tmux keybindings are a bit awkward, but my coworker Dave turned me on to a cool scheme for making them (and Vim keybindings) easier:

1. Rebind the `prefix` key sequence from **Ctrl-B** to **Ctrl-A**
2. Change **Caps Lock** to send **Ctrl**.  This makes `prefix` trivial, *and* makes all of the Ctrl-based keystrokes in Vim super-easy.

Decisions, Decisions
-----
So, do I keep "Hyper Key" behavior, or rebind to Ctrl?  Is there a way to reconcile them all?  I'd love to hear your ideas!
