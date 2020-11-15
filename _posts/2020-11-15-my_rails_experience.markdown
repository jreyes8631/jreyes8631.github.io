---
layout: post
title:      "My rails experience"
date:       2020-11-15 15:08:43 +0000
permalink:  my_rails_experience
---


At the start of this project, I read a lot of posts from different users looking for tips on how to handle this. The most common trend between users was the lack of planning because there is too much what you can do to build an app with rails. I took a pencil and started writing in my code notebook, viewing the nonexistence app in my head. 

After a few hours of research and planning, I started my Project and, it when well. On the first day, I had my database and model up and running. The only thing that I was worry about was using the ''omniauth gem'' luckily I've found a post that helped a lot with a nice guide "https://medium.com/@jenn.leigh.hansen/google-oauth2-for-rails-ba1bcfd1b863" I hope this helps you as it did with me.

I have a full-time job and by the time I was out, I was very tired and just worked a few hours on my project. It was on the weekends that I had the whole day for me and was able to work harder. One tip I can hive you guys is to read a lot about relations, associations, and query methods on rails.

I'm going to leave an example for a scope method.
```
class Review < ApplicationRecord
  	belongs_to :user
  	belongs_to :movie


 	 def self.most_recent
   	 	order('created_at DESC')
  	end

end
```
When I call most recent on my review index or show action it will sort the results showing the most recent one at the top. As an example, this is how I call this on my nested index review action:
" @reviews = @movie.reviews.most_recent ".

Let's see what the future has prepared for me going into Java script.
