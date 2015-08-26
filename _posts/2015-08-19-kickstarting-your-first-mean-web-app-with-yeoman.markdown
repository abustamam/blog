---
layout: post
title: "Kickstarting your first MEAN web app with Yeoman"
date: 2015-08-19 21:42:32 -0700
comments: true
tags: mongodb, express, angular, node, fullstack, yeoman
categories: write-ups
---

I've been going through [Free Code Camp](http://www.freecodecamp.com) and after finishing the front-end "ziplines" (which require a writeup of their own, eventually) I'm finally getting set for the fullstack "basejumps."

However, on their ["Get Set" module](http://www.freecodecamp.com/challenges/waypoint-get-set-for-basejumps), I ran into some problems with Cloud9 (primarily the memory issue), so I decided to figure out how to do some of these things on my local machine.

<!-- more -->

This is primarily a document for me to refer to when I create more fullstack apps, but may as well share it.

Note that I am using OS X. I provide no guarantees in this document, as I'm writing it as it worked for me. Feel free to leave a comment though.

## Step 0: get your environment set up

You should have the following installed: [npm](https://www.npmjs.com/), [Homebrew](http://brew.sh), and probably [bower](http://www.bower.io). Follow the links to install them.

Next, you should install [nvm](https://github.com/creationix/nvm) by running the following script in your terminal:

using curl:
`curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.26.0/install.sh | bash`

or Wget:
`wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.26.0/install.sh | bash`

The stablest node is `node v0.12.7` as of this writing.

I'm going to assume that you are in your project directory now. My project directory is `/sample` so keep that in mind going forward.

## Step 1: Get Yeoman started up

Copy this into your terminal. Note that you must replace [YOUR_USERNAME_HERE] with your username:

`echo "export NODE_PATH=$NODE_PATH:/Users/[YOUR_USERNAME_HERE]/.nvm/versions/node/v0.12.7/lib/node_modules/npm/" >> ~/.bashrc && source ~/.bashrc && npm install -g yo grunt grunt-cli generator-angular-fullstack && yo angular-fullstack`

This will install grunt, grunt-cli, and yeoman's Fullstack Angular generator.

If the installs go well, Yeoman will start up and it will ask you questions. Answer as follows (feel free to answer however you want, but this is how I did):
```
What would you like to write scripts with? JavaScript

What would you like to write markup with? HTML

What would you like to write stylesheets with? CSS

What Angular router would you like to use? ngRoute

Would you like to include Bootstrap? Yes

Would you like to include UI Bootstrap? Yes

Would you like to use MongoDB with Mongoose for data modeling? Yes

Would you scaffold out an authentication boilerplate? Yes

Would you like to include additional oAuth strategies? Twitter

Would you like to use socket.io? No

May bower anonymously report usage statistics to improve the tool over time? (Y/n) Y
```

If the last step fails (the `bower install` and `npm install`) then run it manually:

`bower install && npm install`

## Step 2: Install MongoDB

This part was complicated. But here we go.

First, install MongoDB (I used Homebrw):

`brew install mongodb`

IF all goes well, type the following into your terminal:

`mkdir data && echo 'mongod --dbpath=data --nojournal --rest "$@"' > mongod && chmod a+x mongod`

Note that the Free Code Camp tutorial has this extra line: `--bind_ip=$IP`, which didn't work on my machine. I will find out soon enough if omitting it causes any problems.

Now, to start your database, just run...

`./mongod`

Easy as pie.

## Step 3: Start your server

This one is easy:

`grunt serve`

A new window should automatically open up with Yeoman saying "Allo Allo!"

## Step 4: Set up git

Simple too:

`git init && git add . && git commit -am 'initial commit'`

Then log into your github, and create a new repo, and use the instructions for pushing an existing repo onto github.

It'll look something like this:

```
git remote add origin [YOUR_GITHUB_REPO]
git push -u origin master
```

Yippee. Done!

## Step 5: Set up Heroku

Make an account on [Heroku](http://www.heroku.com) (you might need to enter CC info to use MongoDB), and then type the following into your terminal:

`npm install grunt-contrib-imagemin --save-dev && npm install --save-dev && heroku login`

Then run

`yo angular-fullstack:heroku`

Follow the prompts to get Heroku up and running!

Finally, to set up MongoDB, run the following:

`cd dist && heroku config:set NODE_ENV=production && heroku addons:create mongolab`

Incidentally, you can open heroku from the `dist` folder by simply running `heroku open`.

Now, your Angular Fullstack app is good to go. Best of luck with your new app!
