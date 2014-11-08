---
title: Running All Go Tests in a Project
tags:
- golang
- testing
date: 2014-08-16 08:00:00
layout: post
---

I've been using [GoConvey](https://github.com/smartystreets/goconvey) to run my Go test suite, but kept the `*_test*` files in my `main` package, because I couldn't figure out how to run them all at once from the shell using `go test`.  Yeah, I could have done it in three lines of bash, but that's cheating.

This weekend I finally found `go test ./...` which runs all tests for all packages.  About time.  Test hierarchy fixed!