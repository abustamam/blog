---
layout: post
title: "One Month Stripe Payments Part 1"
date: 2014-08-17 20:26:36 -0700
comments: true
tags: rails, one_month
categories: rails
---

I first started coding with One Month Rails. It was a very simple tutorial to go through, and it took me a month to go through it.

Now, [One Month Stripe Payments has been released](http://mbsy.co/onemonth/10032515). I finished it in a week. 

<!-- more -->

The finished product can be viwed [here](http://calm-everglades-6719.herokuapp.com). I edited a few things of course, I just wanted to get a feel of how things worked.

Now, I'm re-coding the project to make a website for a friend. You can follow along with the [Github repo](https://github.com/abustamam/stuart_welch)

First, to start, I learned something the hard way. Make sure that your project path does not contain any spaces. After probably hours of troubleshooting, I finally elected to change my `Rails projects` directory to `Rails_Projects` and everything worked fine. So don't make my mistake!

Second, here are a list of things you should know about the app:

* Ruby version: 2.1.0
* Rails version: 4.1.1
* Using sqlite3 for development
* Using pg for production (in Heroku)
* Using haml

You're free to make the app in whichever way you'd like, of course. But this write-up will be following those constraints. Your Gemfile should look something like this:

``` ruby Gemfile
source 'https://rubygems.org'
source 'http://gems.github.com'

ruby '2.1.0'

# Bundle edge Rails instead: gem 'rails', github: 'rails/rails'
gem 'rails', '4.1.1'
# Use sqlite3 as the database for Active Record in development and test
gem 'sqlite3', group: [:development, :test]

# Use postgres as the database in production
gem 'pg', group: :production

# Add 12 factor for Heroku
gem 'rails_12factor', group: :production

# Use bootstrap
gem 'bootstrap-sass'

# Use SCSS for stylesheets
gem 'sass-rails', '~> 4.0.3'

# Use Uglifier as compressor for JavaScript assets
gem 'uglifier', '>= 1.3.0'

# Use CoffeeScript for .js.coffee assets and views
gem 'coffee-rails', '~> 4.0.0'

# Use figaro for securely managing credentials
gem 'figaro'

# Use jquery as the JavaScript library
gem 'jquery-rails'

# Turbolinks makes following links in your web application faster. Read more: https://github.com/rails/turbolinks
gem 'turbolinks'

# Build JSON APIs with ease. Read more: https://github.com/rails/jbuilder
gem 'jbuilder', '~> 2.0'

# bundle exec rake doc:rails generates the API under doc/api.
gem 'sdoc', '~> 0.4.0',          group: :doc

# Spring speeds up development by keeping your application running in the background. Read more: https://github.com/rails/spring
gem 'spring',        group: :development

# Use haml
gem 'haml'

# Add stripe for payment processing
gem 'stripe', :git => 'https://github.com/stripe/stripe-ruby'

# Use letter opener in dev
gem 'letter_opener', :group => :development

# Use Automated Admin System
gem 'activeadmin', github: 'gregbell/active_admin'

# Use devise
gem 'devise'

# Use ActiveModel has_secure_password
gem 'bcrypt', '~> 3.1.7'
```

Since we're using `pg` instead of `sqlite3` as our database, let's remove it from the production part of the database file.

Run `bundle install --without production` and you should be ready to run!

Go ahead and make your new rails app:

`rails new stripe_payments`

The first thing you'll want to do is configure your home page. 

``` ruby app/controllers/pages_controllers.rb
class PagesController < ApplicationController
   def home 
   end 
end
```

Quick way to do this is to run `rails g controller pages` and the `pages_controller.rb` file will automatically be generated. 

Make the routes point to it:

``` ruby config/routes.rb
Rails.application.routes.draw do
  root 'pages#home'
end
```

Now, create your home page. Remember I'll be using HAML. The tutorial uses ERB. Use whichever suits your fancy.

``` html app/views/pages/home.html.haml
Hello world!
```

At this point in the One Month Stripe Payments Tutorial, Chris "steals" (I mean borrows!) his own design from another one of his repositories. Of course there's nothing wrong with it, since he's using his own design. The next couple of days are focused on establishing the functionality of the page that it's supposed to have. That being said, let's just copy the finalized design and skip the legwork.

Here are the files you'll want to look out for:

* app/views/layouts/application.html.haml
* app/views/pages/home.html.haml
* app/assets/ (everything inside)
* config/environment/production.rb 

In that last file, the following changes were necessary:

* Change `config.assets.compile` to `true`
* Uncomment `config.action_dispatch.x_sendfile_header = 'X-Accel-Redirect'`
* Change `config.assets.digest` to `true`

This was to make the assets work on Heroku.

Again, here is the [Github repo](https://github.com/abustamam/stuart_welch).

All in a day's work right? Tomorrow we'll finish adding Stripe functionality and we'll be done, hopefully!





























