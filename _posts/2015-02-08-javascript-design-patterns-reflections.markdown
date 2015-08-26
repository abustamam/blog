---
layout: post
title: "Javascript Design Patterns Reflections"
date: 2015-02-08 16:14:46 -0800
comments: true
categories: front-end, learning, nanodegree
---

Rundown
===

This course focuses on Javascript design patterns. It takes us through several simple projects for the sake of learning good design patterns. I will post my brief reflections of each project here. 

<!-- more -->

# Cat Clicker

[Cat Clicker](/Cat-Clicker) was my first project. 

## version 0.1

Has one single cat. It was very easy to set up, just getting the structure of the HTML page I need to get used to. 

I feel pretty good about my code, even though it's not "beautiful."

I clicked my cat probably 10 times to test functionality. 

## version 0.2

Since the HTML skeleton is already available for me, I merely dumped both cats into a `#cats div` and added a class for each cat. 

I still feel good about my code, though it's still not beautiful. 

Clicked probably another 10 times to test functionality. 

## version 0.3

Finally, I added 5 cats, and each cat has its own click-counter. 

It took WAY too long for me to figure out how to do it, but using classes seemed to be the way to go. Now, as long as I have the pics, I am able to add as many cats as I want!

## version 0.4 

Using MVO, I was able to abstract my code to separate concerns. However, in simplifying my Model, I introduced a bug (which I will fix)...

- When opening app for the first time and clicking on kitten 0 a few times, switching to one kitten then back to kitten 0 resets kitten 0 back to 0 clicks, first time only. Cause is likely currentCat.

- When clicking reset button, and switching to another cat that has clicks (without refreshing), cat will still display its old number of clicks. A refresh will fix this. Cause is likely the fact that switching cats uses a copy of currentCat, and the copy's clicks are not reset. Since the scope of the cat copy is limited to the IIFE, I will try to determine a workaround. 

## version 0.4b

Bugfix: all kitten data are synced with local storage (saves on each click)
Bugfix: Reset button works properly

## version 0.5

Add admin panel, which allows "cheating" (aka changing number of clicks)

## version 1

Uses knockout.js, looks cool

# School-Attendance App

Original Udacity repo is [here](https://github.com/udacity/ud989-school-attendance). My repo is [here](https://github.com/abustamam/school-attendance).

The goal of this app is to refactor existing code from spaghetti code into maintainable code using MVO, which was done pretty easily. The model was the list of students and the days they missed. The view was how the app looks. And the octopus was what bound everything together. 