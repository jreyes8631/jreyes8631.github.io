---
layout: post
title:      "React, Rails and Redux"
date:       2021-03-28 13:50:22 +0000
permalink:  react_rails_and_redux
---


I wanted to start by saying thank you all! I feel grateful for all the people that somehow made an impact on my life in this course. I've been putting in the work since day one and, it has paid off.

For this final project, I decided to re-invent an application I made in Ruby on Rails portfolio project, a movie review app, it's something that I will continue to work on and someday can release to the public like IMDB or Rotten tomato.

I started with my backend creating my rails app API only. 
```
rails new movie-review-backend --api
```
running the previews command will allow you to create a ruby app with no HTML rendering. You can remove the files you are not going to use such as views and them, Change your ApplicationController to inherit from ActionController::API
```
class ApplicationController < ActionController::API
end
```
make sure to add the ''config.api_only = true'' to config/application.rb file:
```
class Application < Rails::Application
    config.load_defaults 6.0
    config.api_only = true
  end
```
When you start generating files with ''rails generate'' this will identify ad create API only controllers and when using the scaffold this will automatically come pre-build with JSON response.  

now bundle install the gem 'rack-cors' to configure your cors.rb as follow.
```
Rails.application.config.middleware.insert_before 0, Rack::Cors do
  allow do
    origins '*'
    resource(
     '*',
     headers: :any,
     expose: ["Authorization"],
     methods: [:get, :patch, :put, :delete, :post, :options, :show]
    )
  end
end

```
Now you have your API-only rails app.  Working with React and redux was fun but it was challenging too, however, with practice and dedication we all can achieve greatness.
