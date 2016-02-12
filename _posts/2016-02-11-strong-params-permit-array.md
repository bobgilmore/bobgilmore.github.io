---
title: Strong Params and Arrays of Values
tags:
- rails
date: 2016-02-12 10:35:00
layout: post
---

The Strong Parameters `#permit` method only allows permitted *scalar* values by default. See [the documentation on permitted scalar values]( https://github.com/rails/strong_parameters#permitted-scalar-values).

Here's the important bit that I always forget:

> To declare that the value in params must be an array of permitted scalar values map the key to an empty array:

`params.permit(:id => [])`
