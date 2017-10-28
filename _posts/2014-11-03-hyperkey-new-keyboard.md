---
title: Diagnosing Hyperkey Problems
tags:
- tmux
- unix
- productivity
date: 2014-11-04 08:00:00
layout: post
---

A few months ago I posted about [creating a Hyper key](/2014/03/13/tmux-hyper-caps.html).  I live off of it, especially when using Vim and Tmux, but the darn thing keeps breaking!

Twice, I've tracked it down to switching keyboards.  The settings that you change in [Seil (formerly PCKeyboardHack)](https://pqrs.org/osx/karabiner/seil.html.en) only work if you turn the Caps Lock behavior in the Keyboard Control Panel.  But that setting is made on a *per-keyboard* basis, so swapping in a new keyboard might reactivate Caps Lock.

To fix it,

1. Go to *System Preferences - Keyboard*
2. Select the *Keyboard* tab
3. Select *Modifier Keys...*
4. In the sheet that appears, select your current keyboard
5. Set *Caps Lock* to *No Action*
