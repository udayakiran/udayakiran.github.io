---
layout: post
title: "Javascript - moment.js (Best way to deal with dates in js)"
description: "Javascript library - moment.js: Play with date objects comfortably including in different locales and time zones."
tags: [javascript, programming, web, js library]
image:
  feature: abstract-6.jpg
  color: "8749D8"
  icon: "clock-o"
bg_color: "8749D8"
---

## Why ?

- Ring js helps to create class system which supports multiple inheritance in a classical object oriented way.
- As such , javascript supports prototypal inheritance which is not that flexible in supporting multiple inheritance or mixin way of reusing classes which is addressed by this.
- Ring js is inspired by python's classical multiple inheritance system.

## Info -

* Home page - <http://ringjs.neoname.eu/>
* Source code - <https://github.com/nicolas-van/ring.js>
* Documentation / Tutorial - <http://ringjs.neoname.eu/docs/tutorial.html>

## Example -

Will try to explain the simple example on ringjs's home page. (Please check the tutorial before trying this. One needs to include underscore.js and ring.js to run the below code.)

### 1. Simple example -

{% highlight javascript %}

// Lets try to create a 'SpiderMan' class which is extended from the classes 'Spider' and 'Man'

//create class 'Human'
var Human = ring.create({
    talk: function() {      
        return "hello";
    },
});

//create class 'Spider'
var Spider = ring.create({
    climb: function() {
        return "climbing";
    },
});

//create class 'SpiderMan' which inherits from "Spider" and "Man"
var SpiderMan = ring.create([Spider, Human], {
    talk: function() {
        return this.$super() + ", my name is Peter Parker";
    }
});

var spiderman = new SpiderMan();
console.log(spiderman.talk());    // prints "hello, my name is Peter Parker"
{% endhighlight %}

###2. One more example -

As an obvious doubt what if both 'Spider' and 'Human' classes both have a function with the same name. Lets try the below example.

{% highlight javascript %}

var Human = ring.create({
    talk: function() {      
        return "hello, my name is Peter Parker";
    },
});
var Spider = ring.create({
    talk: function() {
        return "chirping....";
    },
});

var SpiderMan = ring.create([Spider, Human], {
    talk: function() {
        return this.$super();
    }
});
var spiderman = new SpiderMan();
console.log(spiderman.talk());    // prints "chirping....";

Now, lets redefine SpiderMan class and see.


var SpiderMan = ring.create([Human, Spider], {
    talk: function() {
        return this.$super();
    }
});
var spiderman = new SpiderMan();
console.log(spiderman.talk());    // prints "hello, my name is Peter Parker";

//Now, it's clear that the method of the class which is inlcuded first in the oder of inheritance gets called.

{% endhighlight %}

## Open issue / Caution -

- If you look at the source of ring.js `https://github.com/nicolas-van/ring.js/blob/master/ring.js` (around line 28), it has `"use strict";` statement. This can cause some syntax errors on the new versions of javascript compilers which you may not have seen before including this library. More details about strict mode can be found at - <http://www.w3schools.com/js/js_strict.asp> .

  #### Fix -
  Obviously try to fix these syntax errors but if you have too many errors which you cant fix, feel free to edit ring.js's source and remove the '"user strict;"' statement. It should be fine removing this.



> I would say "There are out of count ways to create classes in JS but ring.js is one cool way if you want to write classical style of OO code and take the advantage of multiple inheritance."
