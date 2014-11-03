---
title: Don't Cut Corners On Go Setup
tags:
- golang
date: 2014-08-04 08:00:00
layout: post
---

I set up a [Go](http://golang.org/) development environment last month, and I'm having a great time with it!  ([Mark Bates' advice](http://www.metacasts.tv/?keywords=go) has been awesome!) But when I tried [setting up a GoConvey test server](http://www.metacasts.tv/casts/testing-go-web-apps) I kept getting weird errors, like...

> Potential error parsing output of [...] ; couldn't handle this stray line: flag provided but not defined: -covermode

I tried all kinds of things suggested on various blogs; even [removing Go and installing it from source](http://vidottiblog.wordpress.com/).  Nothing worked.

Turns out that GoConvey is sensitive to the Go configuration, because it has to find certain directories for test and code coverage results.  And I had cut a *major* corner in my setup!

## Set Up the Directory Hierarchy Right ##
The Go documentation [recommends a very specific directory hierarchy](http://golang.org/doc/code.html) for use in development.  For example, your source code should live in 

`$GOROOT/src/github.com/<username>/<projectname>`.

There should also be `bin/` and `pkg/` directories under `$GOROOT`.

I thought, "well, I'm not developing packages to deploy on GitHub yet, so I don't *really* need to do that. I'll just throw Go files any old place. Hey, look, things work!"

**Nope nope nope nope nope**.  Do it right!  Because, hey, what do you know, *tools expect things to be where they belong!*

##  Then Re-Get the Packages ##
So I set up the directories correctly and moved my projects under `$GOROOT/src/github.com/bobgilmore/`, but things *still* didn't work right.  The errors went away, but I got 404's whenever I hit the local GoConvey server.  

I decided that the packages were probably compiled with bad paths, or *something*, so I deleted the contents of my `bin/` and `pkg/` directories and refetched the packages I needed via

`go get [...]`

Bang, problem solved!
