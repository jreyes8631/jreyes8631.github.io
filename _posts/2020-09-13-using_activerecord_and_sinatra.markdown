---
layout: post
title:      "Using ActiveRecord and Sinatra"
date:       2020-09-13 22:46:25 -0400
permalink:  using_activerecord_and_sinatra
---


ActiveRecord and Sinatra changed my whole experience on how to start from scratch writing your code. but when I discover corneal it was a blessing. Thank you, Brian Emory!

It is simple and amazing but, I did encounter some issues due to my inexperience.  I was installing a repo and then running corneal new name_of_my_app. I ended up with two folders with the same name and didn't know how to fix this. Eventually, with the try and repeat process and a tutorial on GitHub, I was able to start.

I was asking my fiance for ideas since I was going to dive into another world. More things to do, being able to learn HTML and CSS. We spoke for over two hours taking notes on some ideas. We are far away now, she is in the Dominican Republic and I'm here in the USA waiting for this pandemic to be over because we want to get married and we did cancel everything we had planned.

She reminded me that she is still keeping all the movie tickets from when we were going out in dates to the movies. We are both fanatics when it comes to movies and even more when it comes to DC or Marvel. Right there she asked me "Can you build an app to keep track of the movies we watch?" and there is when the idea came to life. A movie Journal app.

I started by writing all the things I may need to build this app. I was going to use associations like Has_many, belongs_to. validations and working with migrations. 

This is how my user model looks like:

class User < ActiveRecord::Base
    has_secure_password
    has_many :movies, foreign_key: "user_id"
    has_many :reviews
    validates :email, presence: true, uniqueness: true
end

 my movie model looks like this:

class Movie < ActiveRecord::Base
  belongs_to :user
  has_many :reviews
  validates :title, presence: true
  validates :description, presence: true
end


things where difficult at the beggining, but little by little the app growing. I'm so happy for being part of this community and being able to build my path to a carrier that I actually enjoy.
