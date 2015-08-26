---
layout: post
title: "Compiling OpenCV on a Mac"
date: 2015-05-03 12:25:15 -0700
comments: true
categories: opencv
---

I've been helping my dad out with some OpenCV stuff.

I ran into so many problems trying to compile OpenCV that I'm writing a tutorial on how I compiled it on my Mac. 

<!-- more -->

You can install OpenCV quite simply with Homebrew, using the simple command:

`brew install opencv`

However, most OpenCV tutorials rely on you building it yourself as the directories would then be specific to Homebrew. Plus, you don't get to make customizations to your compilation. 

So let's build it ourselves! I used [this](http://mac-opencv-projects.blogspot.com/2014/01/installing-opencv-on-mac-os-x-1091.html) tutorial, but it wasn't sufficient, so I'm adding what worked for me.

Keep in mind that your mileage may vary. This is my environment: 

Mac OS X Yosemite 10.10.2
Xcode 6.3.1 (6D1002)
OpenCV 2.4.8.0
Homebrew 0.9.5
cmake 3.1.0

So, first you'll want to download the [latest version of OpenCV](http://opencv.org/downloads.html). I used the latest stable, which as of this writing, is 2.4.8.0. Unzip this anywhere (I put it onto my Desktop).

**Note: I've heard bad things happening to people who unzip OpenCV into a directory with a space in it. So, don't do that, just in case.**

Now, for some reason the 2.4.8.0 version of OpenCV throws an error when you try to build it using Clang. So you'll want to change one of the files to the code here: [Fixing the LatestPoints problem](https://github.com/Itseez/opencv/commit/35f96d6da76099d80180439c857a4abe5cb17966)

Go to the following file and replace it with the code in the above link:

`[opencvdirectory]/modules/legacy/src/calibfilter.cpp`

That will save you some headache (it did for me).

Secondly, you'll need CMake. 

`brew install cmake` will work (that's what I used) but if you don't use Homebrew then just download it from the [website](http://www.cmake.org/download/).

CD into your OpenCV directory, make a `build` directory, and cd into that too.

```
$ cd ~/Desktop/opencv
$ mkdir build
$ cd build
```

Then build and install OpenCV:

```
$ cmake -G "Unix Makefiles" ..  
$ make -j8  
$ sudo make install 
```

This will install to /usr/local. Keep this in mind for future reference.
