---
layout: post
title:      "Just When Everything Starts to Click"
date:       2020-08-11 02:35:37 +0000
permalink:  just_when_everything_starts_to_click
---


Working through JavaScript has been quite the experience coming from Ruby and Rails. My initial impression was reminiscent of being in France. I knew a decent amount of Spanish and I knew that there were similarities between the Romance languages, but I could not fully grasp what I was looking at or what was being said to me. Much like the concept of objects in javascript vs hashes in ruby, I knew that I've seen these things before, but I couldn't exactly understand what I was seeing.

I found that tedious repetition of writing JavaScript was the only way to learn. Learning a programming language isn't that different conceptually from learning a spoken language, right? So I worked through the Flatiron curriculum and supplemented my learning through the multitude of free resources available online. Here are my top takeaways after working on this project:

### 1. The Browser Console is your friend
I primarily use the Brave browser for my general internet usage. However, while Brave is based on Google's Chromium web browser. It natively blocks ads and scripts and while I did not get deep into why certain things in my code weren't working properly due to time constraints, I quickly jumped back to Google Chrome while developing.

Most modern browsers allow you to right-click and get into the developer tools. Much like the Rails console, you can test out your code directly in the browser to see if the behavior is what you wanted, or if you are returning the values you intended. The ```console.log()``` and ```debugger;``` utilities are life-savers and I found myself using them every time I called a function or returned a value. It is a tremedous help to test in the console prior to writing out your functions.

### 2. Everything is a Function
Using JavaScript to manipulate behavior on the frontend of a web page generally requires that everything be a function. Calling functions in the appropriate manner allows you to control what your user sees and can interact with. Because JavaScript loves functions, you can create them in more than one way! if you don't want to write
```
hello = function() {
return "Hello World!";
```
you can use an arrow function to shorten your code to:
```
hello = () => {
  return "Hello World!";
}
```
But wait, there's more! You can even write anonymous functions. Anonymous functions don't have names and are generally stored in variables like `let show = () => console.log('Anonymous function');`. As you can see, the function is an arrow function, has no name, but is stored in the show variable.

### 3. JavaScript is a Swiss-Army Knife
If you've ever seen a swiss-army knife with a ton of tools (they're call those tools functions as well, btw) you may wonder why someone would need two or three different knives or saws. One knife may work, but wouldn't it be better if you had a knife tailored to exactly what you needed? JavaScript gives developers multiple ways to do the same thing (see functions). Whether it's selecting elements, naming variables, or functions there is more than one way you can do it with JavaScript.

While I found it easier to create and deploy webapps completely in Rails, the utility in JavaScript is in crafting and curating the user experience. After all, they are the ones that are going to use your app anyway?
