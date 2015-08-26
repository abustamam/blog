---
layout: post
title: "Code School Angular JS: Part 1"
date: 2014-08-06 20:36:54 -0700
comments: true
categories: [Angular JS, write-ups]
tags: [AngularJS, CodeSchool, Companion, write-ups]
---

I've been going through the [Shaping Up with AngularJS](http://campus.codeschool.com/courses/shaping-up-with-angular-js/) 
course and decided to share a bit about what I've been learning. 

<!--more-->

I feel the best way to learn is to teach. So I'm doing a write-up of the course, adding in some explanations for the
challenges, and adding some mini-assignments to keep you on your toes, and for you to check your own understanding. 
 
This write-up is not meant to be a replacement for the Code School course; but merely a companion. That being said, 
it's also written textbook-style--if you have this document with you, you can read through it and test yourself 
pretty easily. If you have pen and paper, you can also do all of the challenges. No need for an interpreter or 
anything. The challenges and mini-assignments are small enough for you to be able to write everything down, simply to
test your understanding. 

This is part 1 of the series, which will go over installing Angular (and Bootstrap) and setting up our first controller.

If you want to be able to share your project, go ahead and do Lesson 0; if you just want to run the app locally on your
machine, skip to Lesson 1. Code School does not go over deploying git, so it might be helpful to follow along. 

[TL;DR](#tldr)

## Lesson -1: What is Angular? ##

Angular is...

> A client-side Javascript framework for adding interactivity to HTML.

Angular uses a couple of things in order to achieve this--Directives, and Modules.

> A Directive is a marker on a HTML tag that tells Angular to run or reference some JavaScript code.

Basically, it's an HTML property. It looks something similar to this:

``` html Directive example
<body ng-controller = "StoreController"></body>
```

The `ng-controller` bit is the `directive`.
 
A `module` is where we write pieces of our application. Then we join them together like Lego.
  
Using modules allows us to write testable, readable code. It also defines dependencies, as modules can use other
modules! 

Now that you know what Angular is in a nutshell, continue on to set it up!

## Lesson 0: Set up Angular and Bootstrap ##

This step can be tricky, since there are a few ways to install Angular and Bootstrap. 

### The easy way: using CDN ###

You can simply add the following code to your `head`:

    <script type='text/javascript' src="//ajax.googleapis.com/ajax/libs/angularjs/1.2.21/angular.min.js"></script>
    <link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">

Keep in mind that the code will not work locally unless you type `http:` before all of that.

### The hard way: using Bower ###

Okay, the hard way isn't really that hard, it just requires you to install Node/npm, then `npm install -g bower`, then 
`bower install bootstrap` and `bower install angular`. I won't go into that since it's not the purpose of this post,
but feel free to reach out if you get stuck. 

Your assets will then be thrown into `/bower_components` so make sure that your `head` reflects that.
 
### Deploying live ###

In your command line, just type `git init` and follow GitHub's instructions to push your code up! 

If you want to deploy it live, then create a new branch called `gh-pages`:

    $ git co -b gh-pages

And then commit everything, and when you go to `[your_username].github.io/[your_project_name]` it will be live.
 
If you need additional info feel free to drop a line! 

Mine is currently [here](http://abustamam.github.io/FlatLanders).

## Lesson 1: Setting up `app.js`, `index.html` and our first controller ##

The goal for this course is to make an app so that the Flat Landers can sell some gems! Hey, I don't make the 
stories here. So let's get our storefront set up and ready for money! 

### Your first module ###

Create two new files; `app.js` and `index.html`. 

The first thing we need to do is create our first module! This is simple. Add the following to `app.js`:

    var app = angular.module('gemStore',[]);

Okay, we've created our module. Now we need to _bind_ it to our html.

Begin your `index.html` like so:

``` html index.html
<!DOCTYPE html>
<html ng-app='gemStore'>
  <head>
    <!-- link and script tags may vary depending on how you decided to obtain bootstrap and angular --> 
    <link rel="stylesheet" type="text/css" href="bootstrap.min.css" />
    <script type="text/javascript" src="angular.min.js"></script>
    <script type="text/javascript" src="app.js"></script>
  </head>
  <body>
    <h1></h1>
  </body>
</html>
```

Notice the new `ng-app` property in the `html` tag. This is a `directive` in Angular. Get used
to using them; it's how we'll be 'attaching' things to HTML. Eventually we'll be making our own custom directives,
but for now we'll use some built-in ones. 

You can name your `ng-app` whatever you want, as long as it matches 
the `app` variable in in `app.js`!
    
And there you have it! You are now running Angular. You don't need to use a server in order to view how things look. 
You can simply preview `index.html` in your browser. 

To test it out, go ahead and write some code between the `h1`s:
``` javascript app.js
    ...
    <body>
        <h1>{{"Hello, Angular!"}}</h1>
    </body>
    ...
```
    
Now, you can run JavaScript code between double curly-braces! Try different things out! 

### Your first controller ###

We're making a Gem store. So, we need some Gems to sell! 

We're going to update our `app.js` to do a couple of things. First, we're going to wrap everything into a closure like 
so:
 
``` 
(function(){
    code
})();
```

We can't have a store without stuff to sell, so now, we're going to add stuff to sell! Let's create a gem. Right now, we want to keep things simple, so let's
just make it so our gem has a Name and a Price. Bringing the basics back to shopping! 

The gem will go within the anonymous function. 

``` javascript app.js
var gem = { 
    name: 'Azurite', 
    price: 2.95
};
```

<a name="mini1"></a>

#### Mini-assignment 1: see if you can add a description property to the `gem` variable! ####
 [Click for answer](#minisol1)

But how do we get data from the gem onto the page?

That's where controllers come in.

#### What's a controller? ####

Good question. 

According to Code School, 

> Controllers are where we define our app's behavior by defining functions and values

Basically, it's a way for us to _abstract_ the programming logic from the page into our script.
Thus, we can grab functions and values from `app.js` and insert them directly into our `index.html` page. 

First, we gotta make our controller. The code for a controller is simply:

``` javascript Controller Creation
app.controller('[ControllerName]', function(){
    this.property = "foo"
});
```

Keep in mind that everything you write in the controller belongs to the _scope_ of the controller. I sometimes forgot
that, so watch out! 

Second, you need to _bind_ the controller to your html. This takes place with a `directive`!

``` html Controller Binding
<tag ng-controller = "[ControllerName] as [Alias]">
</tag>
```

You need to create an alias for the controller in order to use it. It doesn't matter what the alias name is, as long
as you use the alias.

Before we move on, let's try these mini-assignments first. 

<a name="mini2"></a>

#### Mini-assignment 2: How would you create a controller called 'StoreController'? ####
 [Click for answer](#minisol2)

<a name="mini3"></a>

#### Mini-assignment 3: How would you bind the controller to a `body` tag with alias of 'Store'? ####
 [Click for answer](#minisol3)

Should have been pretty easy for a smart cookie like you!

You can bind the controller to any tag, but you won't be able to use the controller outside the scope of the tag. So
consider the following example:

``` html Controller Example
<section id ="works" ng-controller = "StoreController as store">
    <div class="foo">
        {{store.product}}
    </div>
</section>

<section id = "nowork" >
    <div class="bar">
        {{store.product}}
    </div>
</section>
```

Anything within the `works` section will parse properly. Anything within the `nowork` section will not parse. 

### Built-in directives ###

Remember, we can think of a `directive` as an html tag property that extracts data from our JavaScript. Luckily, 
Angular comes with some built-in directives. Eventually, we'll be making our own directives, but you gotta start
somewhere!

We're running a store, and a store has physical quantities. 
If we run out, customers should not be able to purchase! Let's take care of this functionality.

First, let's update our Gem to have a couple more properties:

``` javascript app.js
...
var gem = {
    name: 'Azurite',
    price: 110.50,
    canPurchase: false,
    soldOut: true
};
...
```

The key names should be self-evident.

I'm going to introduce you to a couple of built-in directives: `ng-show` and `ng-hide`. 

Let's go over briefly how to use these two directives. `ng-show` and `ng-hide` work similarly; with `ng-show` the tag
will never display unless the code in the directive evaluates to true, and with `ng-hide` the tag will always display
unless the code in the directive evaluates to true. 

That being said, try this mini-assignment to test your wits!

<a name="mini4"></a>

#### Mini-assignment 4: Which tags will display? Which will be hidden? ####

``` html mini-assignment 4-1
<a href="#" ng-show="store.product.canPurchase"> Add to Cart </a>
```
``` html mini-assignment 4-2
<a href="#" ng-hide="store.product.soldOut"> Add to Cart </a>
```
``` html mini-assignment 4-3
<a href="#" ng-show="store.product.soldOut"> Add to Cart </a>
```
``` html mini-assignment 4-4
<a href="#" ng-hide="store.product.canPurchase"> Add to Cart </a>
```

Hint: keep in mind that `canPurchase` is `false`, and `soldOut` is `true`.

 [Click for answer](#minisol4)

Great work! 

Now try this challenge! 

<a name="mini5"></a>

#### Mini-assignment 5: Use directives to achieve the following goals for the following code:

- Button will not show when the product's `canPurchase` property is `false`
- .product div will not show when the product's `soldOut` property is `true`

``` html mini-assignment 5
<div class="product row">
  <h3>
    {{store.product.name}}
    <em class="pull-right">${{store.product.price}}</em>
  </h3>
  <button>Add to Cart</button>
</div>
```

 [Click for answer](#minisol5)
 
### Do it again and again and again and... ###

We're running a store. A store with only one thing to be sold is kind of boring. Let's add a few more gems, like so:

``` javascript app.js
...
app.controller('StoreController', function(){
   this.products = gems; 
});

var gems = [
    { name: 'Azurite', price: 2.95 },
    { name: 'Bloodstone', price: 5.95 },
    { name: 'Zircon', price: 3.95 },
  ];
...
```

Now we have an array of `gems`: so, in order to get, let's say, Azurite, we'll reference it by its index number. In 
`index.html` we'll reference it like so:
    store.products.gems[0]
    
So in order to format that into a `div`, with name and price, we'll do it like this:
 
``` html
<div class="product row">
  <h3>
    {{store.products[0].name}}
    <em class="pull-right">${{store.products[0].price}}</em>
  </h3>
</div>
```

One down, two to go! 

Our `index.html` will end up looking something like this:

``` html index.html
<body class="container" ng-controller="StoreController as store">
    <div class="product row">
      <h3>
        {{store.products[0].name}}
        <em class="pull-right">${{store.products[0].price}}</em>
      </h3>
    </div>
    <div class="product row">
      <h3>
        {{store.products[1].name}}
        <em class="pull-right">${{store.products[1].price}}</em>
      </h3>
    </div>
    <div class="product row">
      <h3>
        {{store.products[2].name}}
        <em class="pull-right">${{store.products[2].price}}</em>
      </h3>
    </div>
</body>
```

Ugh... isn't that annoying? This is like, anti-DRY. 

Luckily, Angular has a built-in directive that allows us to _not_ repeat ourselves. It's aptly called, `ng-repeat`,
and work similarly to how Python loops work (if you're familiar with that).

All we do is alias each recurring 'thing'. If `foo` were an array of objects...

``` javascript foo
app.controller('FooController', function(){
   this.baz = foo; 
});

var foo = [
    { prop1: "cool", 
      prop2: "neat"
    }, { 
      prop1: "awesome", 
      prop2: "gnarly"
    }
];
```

The following expression will iterate through each value in the `foo` array:

``` html bar in FooController
    <a ng-repeat = "bar in FooController.baz">
        <h1>bar.prop1</h1>
    </a>
```

This will create an `<a>` tag for each element in `FooController.baz` (which is the `foo` array of objects we created).

Makes things a lot simpler, huh? 

Let's take this to our store. Try the Mini-Assignment.

<a name="mini6"></a>

#### Mini-assignment 6: Use ng-repeat to make the following html code DRY:

``` javascript app.js
...
app.controller('StoreController', function(){
   this.products = gems; 
});

var gems = [
    { name: 'Azurite', price: 2.95 },
    { name: 'Bloodstone', price: 5.95 },
    { name: 'Zircon', price: 3.95 },
  ];
...
```

``` html index.html
<body class="container" ng-controller="StoreController as store">
    <div class="product row">
      <h3>
        {{store.products[0].name}}
        <em class="pull-right">${{store.products[0].price}}</em>
      </h3>
    </div>
    <div class="product row">
      <h3>
        {{store.products[1].name}}
        <em class="pull-right">${{store.products[1].price}}</em>
      </h3>
    </div>
    <div class="product row">
      <h3>
        {{store.products[2].name}}
        <em class="pull-right">${{store.products[2].price}}</em>
      </h3>
    </div>
</body>
```

 [Click for answer](#minisol6)

Got the assignment? Here's a recap of what we've learned so far...

<a name="tldr"></a>

### TL;DR ###

- A directive is an marker on an HTML tag that tells Angular to run or reference some JavaScript code.
- A controller is where we define our app's behavior, and is bound to the HTML by using `ng-controller`
  - The expression matched to `ng-controller` should match the format: `"[ControllerName] as [Alias]"` and you will
    use the alias to reference the controller throughout.
- Some built-in directives are `ng-hide`, `ng-show`, and `ng-repeat`. 

Okay, neat! Your final code should look something like this. Make sure your code matches before moving onto part 2!

``` javascript app.js
(function() {
  var app = angular.module('gemStore', []);

  app.controller('StoreController', function(){
   this.products = gems; 
  });

  var gems = [
    { name: 'Azurite', price: 2.95 },
    { name: 'Bloodstone', price: 5.95 },
    { name: 'Zircon', price: 3.95 },
  ];
})();

```

``` html index.html
<!DOCTYPE html>
<html ng-app="gemStore">
  <head>
    <link rel="stylesheet" type="text/css" href="bootstrap.min.css" />
    <script type="text/javascript" src="angular.min.js"></script>
    <script type="text/javascript" src="app.js"></script>
  </head>
  <body class="container" ng-controller="StoreController as store">
    <div ng-repeat = "product in store.products" class="product row">
      <h3>
        {{product.name}}
        <em class="pull-right">${{product.price}}</em>
      </h3>
    </div>
  </body>
</html>
```

Note: the `head` in `index.html` may vary depending on how you set up bootstrap and Angular. 

## Assignment Solutions ##

<a name="minisol1"></a>

### Assignment 1 ###

Properties in an object literal is just key: val. Don't forget to put a comma!

``` javascript Mini-Assignment 1 Solution
var gem = { 
    name: 'Azurite', 
    price: 2.95,
    description: "This is the best gem!"
};
```
[Back to assignment](#mini1)

<a name="minisol2"></a>

### Assignment 2 ###

Following the controller definition specs, all we do is use `app.controller`, passing in 'StoreController' and an
anonymous function with the controller properties.

``` javascript Mini-Assignment 2 Solution
app.controller('StoreController', function(){
    this.product = gem;
});
```
[Back to assignment](#mini2)

<a name="minisol3"></a>

### Assignment 3 ###

All we do is add an html property to the `body` tag, and use the `Controller as Alias` format to bind it. 

``` html Mini-Assignment 3 Solution
<body ng-controller = "StoreController as store">
</body>
```
[Back to assignment](#mini3)

<a name="minisol4"></a>

### Assignment 4 ###

Only examples `3` and `4` will display. Remember that `ng-show` tags will only show if the statement 
evaluates to `true`. `ng-hide` tags will only hide if the statement evaluates to `true`. 

[Back to assignment](#mini4)

<a name="minisol5"></a>

### Assignment 5 ###

``` html Mini-Assignment 5 Solution
<div ng-hide="store.product.soldOut" class="product row">
  <h3>
    {{store.product.name}}
    <em class="pull-right">${{store.product.price}}</em>
  </h3>
  <button ng-show="store.product.canPurchase">Add to Cart</button>
</div>
```

[Back to assignment](#mini5)

<a name="minisol6"></a>

### Assignment 6 ###

``` html index.html
<body class="container" ng-controller="StoreController as store">
<div ng-repeat = "product in store.products" class="product row">
  <h3>
    {{product.name}}
    <em class="pull-right">${{product.price}}</em>
  </h3>
</div>
</body>
```

[Back to assignment](#mini6)

