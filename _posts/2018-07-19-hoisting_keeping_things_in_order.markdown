---
layout: post
title:      "Hoisting: Keeping Things in Order"
date:       2018-07-20 03:36:17 +0000
permalink:  hoisting_keeping_things_in_order
---

Regardless of one's knowledge of code, there is a natural order of writing that's universally understood and expected, particulary in the world of journalism:

1.  Introduce the subject (person) of the article with detail.
> **Kendrick Lamar**, reknown rapper...
2.  Describe the action or event of the story, referencing the subject's name (often just last name).
> ... recently received the Pultizer Prize for music. **Lamar** is the first musician to win the prize who is not a classical or jazz musician.

Can you imagine just jumping into the article at line 2? Without a well-defined subject, the article loses meaning and quickly becomes confusing. Just exactly who is this "Lamar"?

In the same way, it makes sense in programming to define our subject  (variable) *before* the action (function) that references it. This is standard practice across languages and makes for easier reading for other developers.

However, JavaScript doesn't read code quite like we do. Instead of reading and running everything at once, the JavaScript engine makes 2 passes over the code. First, it compiles all the *declared* variables and functions. Then, it executes the functions and variable value *assignments*.

This results in some unusual behavior when it comes to JavaScript variables, especially when using **var** . For example:
```
function helloWorld() {
  console.log(message);
 
  var message = 'Hello, world!';
}
```
Invoking this method **helloWorld()** returns *undefined*. Why? Because the variable **message** is not just being declared but also assigned. Since assignment is involved, the JavaScript engine doesn't know what the variable is equal to until after trying to log it to the console.

The JavaScript engine is essentially seeing the following (although we didn't write it this way):
```
function helloWorld() {
  var message;                 // Declaration (value not defined)
	
  console.log(message);        // Logs out 'undefined'
	
  message = 'Hello, world!'    // Assignment (too late to be used)
}
```
This behavior is known as *hoisting*, as it seems to move our variable declaration up the ladder and drop it at the top of the current scope (the function or block in which the variable is declared, or global scope if declared outside a function or block). If we have to use **var**, for example in older codebases, it's possible to avert this behavior by taking the journalism-style writing example from before: declare and assign the variable before it needs to be used.
```
function helloWorld() {
  var message = 'Hello, world!';

  console.log(message);
}
```
The same can be said when using **const** or **let**, but these more modern forms of variable declarations won't even allow themselves to be referenced before assignment and will throw an error such as *"ERROR: Uncaught ReferenceError: message is not defined"*.

In the end, the safest bet is use **const** or **let** where possible, do the hoisting yourself by putting variables at the top of the appropriate scope, and let JavaScript handle the rest!

![](https://media.giphy.com/media/mlJXmW4jdn2tW/giphy.gif)
