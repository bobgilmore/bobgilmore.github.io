---
title: An Auto-Expanding CDPATH
tags:
- git
- unix
date: 2014-12-03 08:00:00
layout: post
---

`$CDPATH` is a great tool on Unix (including Mac).  It's an environment variable that improves `cd`, by letting you go to certain "far-away" directories without typing the whole path to get there.  

There's a good, succinct [description from our neighbors at Bocoup](http://bocoup.com/weblog/shell-hacking-cdpath/).  It also mentions using `bash-completion` to make it even more useful.  Check out the [Pivotal Labs blog](http://pivotallabs.com/cdpath-bash-completion-in-osx/) for details.

`$CDPATH` is good on its own, but not *great*.  To use it, you have to hard-code the *parents* of the directories that you want easy access to (yeesh!) into one of your bash (or zsh) dotfiles.  That's a pain, especially since I share dotfiles across machines.

But wait&hellip; standardization to the rescue! 

Remember [last time](http://blog.bobgilmore.name/2014/12/01/organizing-code.html), when I mentioned that I keep my code projects in a predictable hierarchy?  They're all of the form `$HOME/code/organization_name/project_name`.  So, I put this in my `~/.bashrc`:

    # Add all code repos (if they exist) to the end of CDPATH
    if [ -d "$HOME/code" ]; then
        export CDPATH=".:$(find $HOME/code -type d -depth 1 -maxdepth 1 | tr '\n' ':')"
    fi
    # Initialize bash_completion if it's available
    if [ -f $(brew --prefix)/etc/bash_completion ]; then
        . $(brew --prefix)/etc/bash_completion
    fi

That `export CDPATH` line expands out to include *all* of the directories one level deep in $HOME/code. Since *those* directories include all of my coding projects, well, now they're all just one `cd` away.  Between that and `bash_completion`, command line navigation just got super-easy!
