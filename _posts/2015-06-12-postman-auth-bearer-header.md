---
title: Postman and Authorization Bearer tokens
tags:
- oauth
date: 2015-06-12 13:30:00
layout: post
---

The Jawbone API (among others) uses an [`Authorization Bearer` token](https://developers.google.com/gmail/markup/actions/verifying-bearer-tokens) in the header to [specify the user's `access_token` ](https://jawbone.com/up/developer/authentication).  

So if you're using [Postman](https://www.getpostman.com/) to debug your API access, how do you use the Postman UI *specify* a `Bearer token` in the `Authorization` header?

* Click the Headers button
* Set a `Header` to `Authorization`
* Set its `Value` to `Bearer USERSACCESSTOKENGOESHERE ` .  That is,
    * `Bearer`
    * followed by a space
    * followed by the user's access token

Here's a screencap of Postman in action:

![Postman with Authorization Bearer in the header]({{ site.url }}/img/postman_authorization_bearer_screencap.png)

