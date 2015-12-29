---
layout: post
title: "Javascript - uderscore.js (Functional power to js, without side effects)"
description: "Javascript library - Underscore.js: Get wholesome of functional methods without extending any built-in objects."
tags: [javascript, programming, web, js library]
image:
  feature: abstract-6.jpg
  color: "ee9654"
  icon: "clock-o"
bg_color: "ee9654"
---

## Why ?

- Underscore js is nothing but a simple js library that gives a number of js functional programming helpers which can be used in your js code. It works well with your own js libraries like prototypejs, jQuery or backbone.
- Simplifies your code to a good extent. Well defined functional helpers are a great advantage for programming languages like python and ruby. Underscore does the same for JS.
- More importantly, it does not modify any built-in objects to add these methods. In the practical scenario, we use multiple libraries from different authors. It is important that built-in objects are not extended in any of this code to avoid side effects. (An example problem caused by extending Array.prototype add adding methods/properties - <http://stackoverflow.com/questions/8859828/javascript-what-dangers-are-in-extending-array-prototype>)
- Easy to get started and makes you productive in minutes.

## Info -

* Home page - <http://underscorejs.org/>
* Source code - <http://underscorejs.org/docs/underscore.html>
* Documentation - <http://underscorejs.org/>

## Important functions -

Underscorejs's home page has the list of functions it offers and they are faily simple to be followed from here. I am just listing down some of them which i think are cool.

| Category | functions |
| -------- | ------- |
| Collection (Array/Object)   | *each, map, reduce, reduceRight, find, where, findWhere, reject, some, contains, invoke, pluck, max, sortBy, groupBy, countBy* |
| Array   | *first, last, rest, compact, flatten, without, union, intersection, uniq, zip, unzip, lastIndexOf, findIndex, range* |
|Objects| *keys, allKeys, values, pairs, functions, findKey, extend, pick, omit, clone, has, isEqual, isMatch, isEmpty, isElement, isArray, isObject, isArguments, isFunction, isString, isNumber, isFinite, isBoolean, isDate, isRegExp, isNaN, isNull, isUndefined* |
| Functions   | *bind, partial, memoize, delay, throttle, once, after, before, compose*   |
| Chaining   | *chain*  |

## Example -

In case of underscorejs, you ll call all the functions on "_" and pass your Objects/variables as arguments.
Note that you need to have underscore.js required in your environment to execute the example below.

{% highlight javascript %}

describe("A spec using beforeAll and afterAll", function() {
  var foo;

  beforeAll(function() {
    foo = 1;
  });

  afterAll(function() {
    foo = 0;
  });

  it("sets the initial value of foo before specs run", function() {
    expect(foo).toEqual(1);
    foo += 1;
  });

  it("does not reset foo between specs", function() {
    expect(foo).toEqual(2);
  });
});
{% endhighlight %}

> I would say "Underscore is no big deal and not needed to be a part of your code base if you don't want. I had written a lot of JS code before finding this and was always comfortable. But once you find this little thing, you ll only realize that it takes a great deal out of your way and makes you happy. Especially, if you know what it means modifying the native objects."
