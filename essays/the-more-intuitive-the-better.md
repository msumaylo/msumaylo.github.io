---
layout: essay
type: essay
title: The More Intuitive, The Better
# All dates must be YYYY-MM-DD format!
date: 2022-02-10
labels:
  - Coding Styles
  - ESLint
  - JavaScript
---

<img class="ui small right floated rounded image" src="../img/ESLint_logo.png">

## Coding standards allow for consistency

In some ways, coding standards are similar to design standards for most other things. As a basic example, we can consider something like letter-size paper. As the user, we know that when we get a pack of printer paper in letter-size, you know that the paper will be 8.5 inches wide, and 11 inches long, and that it will fit into the printers that accept that size. For the manufacturers, having these standards ensures that they know what exactly they are creating. With coding standards, it allows the programmer to have a good idea of what the code they will work with or create should look like, among other desired qualities.
  
## Coding standards make code more readable and intuitive

 To build off the point of consistency and how code should look like, consider two papers with essentially the same content. One paper is written with proper indentation, the text is divided into paragraphs, there are headers, and there are few to no run-on sentences. Conversely, the other one is just one massive paragraph, with many run-on sentences. Both could have the exact same content, but if you had to read the material, you would choose the former. With the former, you would be able to read it and easily follow along with what the writer wanted to convey. Conversely, with the latter, you would easily get lost in the sea of words, and the paper may end up feeling more like a jumble of incoherent ideas.
  
With code, you want to be able to read the code, and be able to follow along with what the code does. When working, you might be working with code made by someone else years ago. If a coding standard was followed, it ensures that you have an easier time understanding what’s going on with the code, and that you don’t have to drag the person who made the code to walk you through each line to understand what it does. 

## Coding standards help with writing code
In addition to making sure your code looks nice, being in the habit of writing readable code can help make it easier to be focused on what you want to write. Instead of having to worry about being able to write readable code, you can focus more on making code that works.

Coding standards also aid in letting you know what you should and shouldn’t do in your code. For example, [ESLint/Airbnb’s JavaScript style guide](https://github.com/airbnb/javascript) will show warnings when using var, or when using let when const can be used instead:
```
2.1 Use const for all of your references; avoid using var. eslint: prefer-const, no-const-assign

Why? This ensures that you can’t reassign your references, which can lead to bugs and difficult to comprehend code.

// bad
var a = 1;
var b = 2;

// good
const a = 1;
const b = 2;

2.2 If you must reassign references, use let instead of var. eslint: no-var

Why? let is block-scoped rather than function-scoped like var.

// bad
var count = 1;
if (true) {
  count += 1;
}

// good, use the let.
let count = 1;
if (true) {
  count += 1;
}
```
As shown in the provided examples, it is beneficial to make use of const instead of var to prevent reassigning references when you don’t want them to be modified. In the case of let, it allows you to reassign references while also having block-scope.

## My own experience with coding standards

At this point, ESLint has been a useful tool for my JavaScript learning experience. In particular, ESLint warnings for using const over let have been useful, as I tend to make use of let for arrays, where const would not affect my ability to push values onto said arrays. Seeing the green check mark in IntelliJ is also satisfying, with the reassurance that my code at least conforms to ESLint’s standards. However, it can be a cause for concern when I have to code in a limited amount of time, but I feel that the standards will become second nature to me the more I make use of it.

