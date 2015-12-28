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
|----
| Functions   | *bind, partial, memoize, delay, throttle, once, after, before, compose*   |
| Chaining   | *chain*  |

## Example -



## Open issue / Caution -

> I would say "There are out of count ways to create classes in JS but ring.js is one cool way if you want to write classical style of OO code and take the advantage of multiple inheritance."
