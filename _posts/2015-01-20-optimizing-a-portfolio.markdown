---
layout: post
title: "Optimizing a Portfolio"
date: 2015-01-20 11:50:41 -0800
comments: true
categories: front-end, learning, nanodegree
---

# Here's the latest

The latest project was to optimize a portfolio. Once I get the project graded, I will update the [portfolio](/mobile-portfolio) to be my own. However, here are some take-home points I got.

<!-- more -->

## The course

[The course](https://www.udacity.com/course/viewer#!/c-ud884-nd) itself wasn't bad. However, it definitely wasn't interesting. 

The course focused on the Critical Rendering Path (CRP) and how to optimize it. However, I felt it didn't go into specifics, like how to optimize above-the-fold CSS. I had to look at resources elsewhere to learn what that was. 

Aside from all that, I did learn a lot from the course, but I feel I learned more from the [Google web fundamentals](https://developers.google.com/web/fundamentals/) guide (incidentally, written by one of the lecturers in the course!).

## The project

The project was to optimize [this portfolio](github.com/udacity/frontend-nanodegree-mobile-portfolio) in two primary ways.

The first goal was to optimize the website such that it got a score of 90+ on [Page Speed Insights](https://developers.google.com/speed/pagespeed/insights/?url=abustamam.github.io%2Fmobile-portfolio). This was done by analyzing the CRP and performing optimizations such as inlining critical CSS and async-ing non-critical scripts. 

The second goal was to optimize the [pizza page](mobile-portfolio/pizza.html) such that it ran at 60 FPS. This was done by performing several JavaScript optimizations.

The main issue I ran into with the project was the task automaters (more on this [below](#gulp)).

The project itself was pretty simple. In fact, though I thought the project would be incredibly boring (make one change, measure, make another change, measure) it certainly wasn't that. 

Granted, I did need to measure the results of each change I made, but it wasn't terrible. In fact, my task-runner did most of the work for me. I just made sure that all my tasks were written correctly. 

The second part of the project was optimizing the JavaScript.

The tough part about this was that I didn't know too much about requestAnimationFrame. So I learned! And that's what life is all about. So I learned about the rAF, and used it to optimize my JavaScript.

Also, I moved variable declarations outside of functions/for loops, if the variables were constant throughout. For example, there will always be x number of pizzas, so why not push that into a variable and iterate over that array? Fewer calculations = better performance.

## Using Gulp.js

I must admit, I started using Grunt first. Then I learned about Gulp and decided to try it out. 

Both of them looked incredibly complicated, but as I played around with them I learned a lot about them, and also about node.js. Though they seemed complicated, they really weren't. 

Since I ended up using Gulp, I won't talk about Grunt. 

With Gulp, all you do is pipe streams of data around. You start with a source, and then you perform a 'task' on it, and you can do whatever you want with the result of that task (even perform another task on it).

When you write your own tasks, you can add task dependencies:

```
gulp.task('one', function(){
  // do something
});

gulp.task('two', ['one'], function(){
  // do another thing
});

gulp.task('three', ['one'], function(){
  // do something else
});

gulp.task('default', ['two', 'three']);
```

The above code has a default task `default`, which depends on 'two' and 'three'. Since both of them depend on 'one', 'one' must finish before 'two' or 'three' begin. However, even though both of them depend on 'one', 'one' is only run once. Neat huh? 

I used this to 'clean' before minification. Each minification task depended on `clean`, which was run before any minification task. So my bulk-minification task `minify` ran clean before running any single minification task. Very handy! 

Now, back to the issues I ran into.

<a name="gulp"></a>
### Imagemin images can't be huge

The first main issue was with `imagemin` which is a great tool, but there was a weird problem.

It was failing with a strange error. 

So I did some trial and error by removing certain files, and I found out that it didn't fail when I took out the huge 'pizzaria' image file. 

I surmised this was because the pizzaria image file was so big, it killed imagemin. So I deleted it, and this worked fine. 

So that brings me to a lesson learned--sometimes you have to do trial-and-error to figure out what's going wrong. 

### Don't forget to change sources!

To simplify my app, I moved all html files to the base (build), and all assets into their respective folders (i.e. img, css, js). I was running into so many errors when I was trying to optimize my pizza page.

It turns out that it was calling the wrong css file! 

So if you're going to restructure your app's directory, make sure that you double check each page's resources! 

## Moral of the story

I learned a lot in this project, namely for task automation. Gulp is definitely a godsend when it comes to optimization, so I was happy to learn it. It took a while, but I finally got it down, and it was awesome! 