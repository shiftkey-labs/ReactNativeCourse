# Intro to JavaScript - JS Stats & Platform

* JavaScript (JS) is a high-level, interpreted programming language. 
* JS is on an 11 year streak as the most popular programming language in the 2023 StackOverflow Survey <!-- .element: class="fragment" -->
* You may be most familiar with JS in the context of the browser, where it’s used to program web pages <!-- .element: class="fragment" -->
* The magic of the language is that it’s ported to so many different platforms <!-- .element: class="fragment" -->
* We’ll be using Javascript to code our React Native apps <!-- .element: class="fragment" -->

---

# Running JS Code (MacOS)

* To best understand JavaScript, you'll want to be able to run JS code on your computer
* Using Homebrew: <!-- .element: class="fragment" --> 
* <code>brew install node</code> <!-- .element: class="fragment" -->
* Make a file with the extension (.js) and execute in Terminal: <!-- .element: class="fragment" -->
* <code>node file.js</code> <!-- .element: class="fragment" -->

---

# Running JS Code (Windows)

* Download nodeJS from https://nodejs.org/en/Download
* Make a file with the extension (.js) and execute in Console:  <!-- .element: class="fragment" -->
* node file.js <!-- .element: class="fragment" -->

---

# JS Variables Introduction

* In JavaScript, variables are containers that store data values
* These values can be of various types, including numbers, strings, booleans, objects, arrays, functions, and more <!-- .element: class="fragment" -->
* Variables in JavaScript are declared using the var, let, or const keywords, followed by the variable name <!-- .element: class="fragment" -->

---

# JS Variables - const

```js 
const x = 10;
x = 20; // not allowed, will throw error
```

* const is used to declare variables whose values cannot be re-assigned
* This is one of the most common ways you'll see React Native variables declared <!-- .element: class="fragment" -->

---

# JS Variables - let & var

```js
let x = 10;
x = 20; // allowed

var y = 5;
y = 6; // allowed
```

* let is used to declare variables whose values can be re-assigned - so is var
* So what's the difference? <!-- .element: class="fragment" -->
* let is distinct from var, in that it has block scope, whereas var has function scope <!-- .element: class="fragment" -->

---

# JS Blocks

```js
const count = 10;

while (i < count) { 
	console.log(i);
	i++;
}
```

* In JavaScript, a block is a set of statements enclosed within a pair of curly braces { }
* Blocks are used to group multiple statements together, and define scope <!-- .element: class="fragment" -->
* Blocks are generally used in tandem with if statements, function definitions, & loops <!-- .element: class="fragment" -->

---

# JS scope

---