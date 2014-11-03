---
layout: post
title: Changing Your Rails Project Name
tags:
- rails
---
A while ago I wanted to change a Rails project name.  Since the project was well underway, it wasn't easy to find the locations.  Where *does* a project's name appear in freshly generated code?  (I studied this under Rails 4.0.0.rc1.)

I found that the project name appears in the following places:

### `app/views/layouts/application.html.erb : 4`

    {% highlight html %}
    <title>ProjectName</title>    
    {% endhighlight %}

### `config/application.rb : 9`

    {% highlight html %}
    module ProjectName
    {% endhighlight %}

### `config/database.yml : various`
1. The database names for all configurations (development, production, and test) are based on the project name.
2. The usernames (if any) in all configurations are the project name.


### `config/environment.rb : 5`

    {% highlight ruby %}
    ProjectName::Application.initialize!
    {% endhighlight %}

### `config/environments/*.rb : 1`

All environment files start with:

    {% highlight ruby %}
    ProjectName::Application.configured do
    {% endhighlight %}

### `config/initializers/secret_token.rb : 12`

    {% highlight ruby %}
    ProjectName::Application.config.secret_key_base = 'the_key'
    {% endhighlight %}

### `config/initializers/session_store.rb : 3`

    {% highlight ruby %}
    ProjectName::Application.config.session_store :cookie_store, key: '_ProjectName_session'
    {% endhighlight %}

### `config/routes.rb : 1`

    {% highlight ruby %}
    ProjectName::Application.routes.draw do
    {% endhighlight %}

### `Rakefile : 6`

    {% highlight ruby %}
    ProjectName::Application.load_tasks
    {% endhighlight %}