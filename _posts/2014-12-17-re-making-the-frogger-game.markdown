---
layout: post
title: "(Re)making the Frogger Game"
date: 2014-12-17 13:40:50 -0800
comments: true
categories: front-end, learning, nanodegree
---

# Six weeks later

I'm back, and I've finally finished my game project, using HTML5 Canvas and JS. You can view the finished project [here](/bugger). 

<!-- more -->

The courses used were [HTML5 Canvas](https://www.udacity.com/course/viewer#!/c-ud292-nd) and [Object-oriented Javascript](https://www.udacity.com/course/viewer#!/c-ud015-nd).

I learned a lot while working through this project. Not only about programming, but also about motivation and getting things done. 

## When you're stuck...

I learned that when you're stuck, just go with your "gut feeling" and see if it works. If it doesn't work, check the errors, and see if you can fix what you broke. 

Always always _always_ work one change at a time if you're "stuck," unless of course you're confident what you're doing is going to work. Here's an example...

At one point, I decided I wanted to add a character selection screen. Up until this point, the canvas was only drawing the main game. In order to add a character selection screen, I needed to add a new "screen." To this effect, I decided to add a "game state" to the game, so that way the engine could track the state of the game and render appropriate content for its state. 

Once I did that, I worked the start screen piece by piece. I started by drawing one character, then the Selector, and then I added more characters. Then I added the logic to the Selector class, and ensured that the Selector responded in the way I wanted it to. Then I ensured the Selector was passing in the chosen character data to the main game, so that it could render the correct character. 

** Bug: Notice that when you choose one of the heroines on the right side, they start on the right side instead of in the middle. I am working on a fix for this. 

I like to imagine development like Lego. You have a plethora of commands and methods at your disposal, you need to use your imagination and iteratively build upwards, until you get what you need. 

## Designing your code

When you use function declarations...

  function () {}

vs 

  var fn = function () {}

...Javascript does something known as "hoisting." Function declarations are loaded _first_, so the order doesn't really matter. 

However, they _do_ matter to you. When you're looking for something that broke, or want to tweak something, you'll want to find it quickly. So it's important to have everything organized in a logical sense, using comments when necessary. As tempted as I was to haphazardly place prototypical functions wherever I wanted to, I made sure that the prototypical functions were neatly organized beneath their respective classes. Perhaps it was my OCD, but it made it immensely easy for me to find everything. 

It also makes it easy for you to keep code in your head. 

## Mustering motivation

I've had the opportunity to work a lot of hours during this project. There were also a lot of family visits, and I managed to get sick twice. That made my motivation to code shot. 

How did I get past humps? 

First, I made a clean workstation. A workstation that is organized allows for an organized mind and thought process. I moved my desk around so it makes me feel like I'm in an office, so I'm tempted to work as if I were in an office. 

Second, I made a list (mental or otherwise) of things I wanted to accomplish. What was my task for today? Was it to add collision detection? Was it to add winning conditions? Was it to add a start/game-over screen? I'd choose one task and hack at it. 

Third, when I felt like I had momentum (or "flow"), I'd stop. This is effective because it allows for your brain to relax (e.g. not think about the problem at hand). The next day, I'd be motivated to pick back up where I started and continue my momentum.

Contrast this with following through with momentum. If the first task to do the next session is difficult, it'll be hard to motivate yourself to do it. So if you make finishing the task easy and push it to the start of the next session, you'll continue your momentum and be able to drive through the difficult task more easily. 

And finally, no workstation is complete without a kitten on your lap.

## What's next?

My next project is to learn website optimization. I'll of course post my results of the next project when I'm done. 

Til next time! 