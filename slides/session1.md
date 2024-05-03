# ShiftKey Academy Up 
## React Native  
### Session 1
### ShiftKey Labs
#### Allan Lavell

---

# Land Acknowledgement

ShiftKey Labs is located in Mi'kma'ki, the ancestral and unceeded territory of the Mi'kmaq people. We are all treaty people.

---

# About ShiftKey Labs

* ShiftKey Labs ( https://shiftkeylabs.ca) is a non-profit, part of the Nova Scotia Sandbox project, hosted in the Dalhousie Faculty of Computer Science
* ShiftKey Labs has 3 primary goals:
1. Creating strong talent for the Nova Scotia technology industry
2. Ensuring that computer science students gain innovation and entrepreneurship experience outside the classroom 
3. Developing deep connections between computer science students and the Nova Scotian tech startup community 

---

# ShiftKey Labs - 5 Programs

1. ShiftKey Sandbox – All of our hackathons / general programming
2. ShiftKey Academy Up - Technical Certifications for up-skilling 
3. ShiftKey Academy – Reimbursement up to $150 CAD for approved technical certifications  (AWS, Azure, GCP & more - Dalhousie students only at present) 
4. ShiftKey Works – Connecting students to part-time work 
5. ShiftKey Build – Supporting student-led startups with funding, mentorship 

---

# Session 1 Overview

* Motivation for learning React Native
* Basic React Native components - Text, Image, View
* Tailwind via TWRNC & Styling
* JavaScript fundamentals - Variables, Functions, Arrays, map
* Intro to JSX - JavaScript eXtensions 

---

# Session 1 Overview

* Writing Custom components
* Props - Passing data into components
* State & useState
* React Hooks - how to add functionality to components
* TouchableOpacity - creating buttons
* TextInput - Entering Text Data 

---

# Session 1 Overview

* SKNotes Course Project App
* Git & Github
* Visual Studio Code
* etc.

---

# Motivation - Cross Platform Development

* With React Native, you can write code once and deploy it across multiple platforms, including iOS and Android
* This dramatically reduces development time and effort compared to building separate native apps for each platform 

---

# Motivation - Familiarity with React

* If you're already familiar with React, learning React Native will be a natural progression
* React Native follows the same principles as and has similar syntax to React 

---

# Motivation - Native Performance

* React Native bridges the gap between native and web development by compiling JavaScript code to native UI components
* This approach ensures that React Native apps deliver high performance and native-like user experiences 

---

# Motivation - Large Ecosystem & Community

* React Native has a vibrant ecosystem with a wide range of libraries, tools, and resources available to developers
* The community is active and supportive, providing valuable insights, tutorials, and open-source contributions to help developers succeed 

---

# Motivation - Rapid Iteration and Prototyping

* React Native's Hot Reloading feature allows developers to see changes in real-time as they code, making it easy to experiment, iterate, and prototype new features quickly
* This rapid development cycle accelerates the feedback loop and enhances productivity 

---

# Motivation - Cost-Effective Solution

* Building mobile apps with React Native can be more cost-effective than traditional native development, especially for startups and small businesses with limited resources
* By leveraging a single codebase for multiple platforms, organizations can reduce development costs and time to market 

---

# Motivation - Job Opportunities & Career Grwoth

* React Native skills are in high demand in the job market, with many companies seeking developers who can build mobile apps effectively
* Learning React Native can open up exciting career opportunities and contribute to your professional growth as a developer 

---

# Diving in - Hello World Text Component

* The simplest component in React Native - Text

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-text-component?iframeId=e8edg84lan&amp;preview=true&amp;platform=web&amp;theme=light" height="250px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe> 

---

# Styling - Tailwind

* To layout and style components, we’re going to use twrnc (Tailwind React Native Classes) - a React Native implementation of Tailwind
* Tailwind is a fast way of declaring styles for components with minimal boilerplate 

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-text-styled?iframeId=gyj1hl4sxk&amp;preview=true&amp;platform=web&amp;theme=light" height="300px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe> 

* Everything in between the tw backticks (note that we’re using backticks - not single quotes!) is tailwind classes, which give you quick access to common styling functionality 

---

# Styling - Tailwind

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-text-styled?iframeId=gyj1hl4sxk&amp;preview=true&amp;platform=web&amp;theme=light" height="300px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

* text-blue-700 sets the text to the color blue-700 (try blue-500, blue-300, etc. for variations) 
* mt-18 sets the margin-top to be 18, pushing the text down 18 units. 
* text-4xl sets the text to be extra large, 4x 

---

# Image

* The React Native Image component is a fundamental building block for displaying images in mobile applications
* It provides a simple and efficient way to incorporate various types of images, including local assets, remote URLs, and base64-encoded images 
<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-image?iframeId=7stcoapwnq&amp;preview=true&amp;platform=web&amp;theme=light" height="300px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# View 

* The View in React Native is a fundamental component that is primarily used as a container for other components
* It doesn’t render anything in its foreground, but can take on a shape as well as background colors / images.
<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-view?iframeId=vxcu7tx148&amp;preview=true&amp;platform=web&amp;theme=light" height="300px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>
* See how in this example we have two Views - one with a background color of black, covering the whole screen, and containing a yellow View with rounded corners

---

# Intro to JavaScript - JS Stats & Platform

* JavaScript (JS) is a high-level, interpreted programming language. 
* JS is on an 11 year streak as the most popular programming language in the 2023 StackOverflow Survey 
* You may be most familiar with JS in the context of the browser, where it’s used to program web pages 
* The magic of the language is that it’s ported to so many different platforms 
* We’ll be using Javascript to code our React Native apps 

---

# Running JS Code (MacOS)

* To best understand JavaScript, you'll want to be able to run JS code on your computer
* Using Homebrew, a package manager for MacOS:  
* <code>brew install node</code> 
* Make a file with the extension (.js) and execute in Terminal: 
* <code>node file.js</code> 

---

# Running JS Code (Windows)

* Download nodeJS from https://nodejs.org/en/Download
* Make a file with the extension (.js) and execute in Console:  
* node file.js 

---

# JS Variables Introduction

* In JavaScript, variables are containers that store data values
* These values can be of various types, including numbers, strings, booleans, objects, arrays, functions, and more 
* Variables in JavaScript are declared using the var, let, or const keywords, followed by the variable name 

---

# JS Variables - const

```js 
const x = 10;
x = 20; // not allowed, will throw error
```

* const is used to declare variables whose values cannot be re-assigned
* This is one of the most common ways you'll see React Native variables declared 
* The reason this works in React, is that React components re-render and that allows for variables to take on new values at that time

---

# JS Variables - let & var

```js
let x = 10;
x = 20; // allowed

var y = 5;
y = 6; // allowed
```

* let is used to declare variables whose values can be re-assigned - so is var
* So what's the difference? 
* let is distinct from var, in that it has block scope, whereas var has function scope 

---

# JS Blocks

```js
const count = 10;

function x() { // Start block
	const a = 0;
	let b = 1;
	var y = 2;
} // end block
```

* In JavaScript, a block is a set of statements enclosed within a pair of curly braces { }
* Blocks are used to group multiple statements together, and define scope 
* Blocks are generally used in tandem with if statements, function definitions, & loops 

---

# JS Scope

* Scope in JavaScript refers to the accessibility and visibility of variables and functions within different parts of the code
* JS has 3 main types of scope: global scope, local scope, and block scope
* Variables declared outside of any function have global scope and can be accessed from anywhere in the code
* Variables declared inside a function have local scope and can only be accessed within that function
* Variables declared with let or const have block scope, and are only visible in the block in which they are declared - this is usually what you want

---

# JS Functions - Function Keyword & Arrow Functions

* Functions in JS are a way of encapsulating actions, which can read and write data
* Functions are typically declared in one of two ways 
* Method 1: the function keyword
```js
function myFunction() {
	console.log("Hello World");
}
```
* Method 2: arrow functions
```js
const myFunction2 = () => {
	console.log("Hello World");
}
```
* It's common practice in React Native to use the arrow function syntax

---

# Calling (or Executing) JS Functions

* You use the name of the function, followed by parentheses, in order to call the function and execute its logic
```js
const myFunction = () => {
	console.log("Hello World")
}

myFunction() // prints Hello World
```

---

# Functions - Parameters & Arguments

* Functions can accept a list of **parameters**, which are variables that get assigned values at the time when the function is called
* This is how you pass data into a function
```js
const print = (x) => {
	console.log(x);
}

print("hey") // logs "hey" to the console
```
* The values passed to functions at the time of calling are called **arguments** - in this example, x is the parameter, and "hey" is the argument

---

# JS Functions - Returning Values

* In order for a function to give a result, it can do what’s called returning a value
```js
const add2 = (x) => {
	return x + 2;
}

const y = add2(4);
console.log(y); // logs 6 to the console
```
* The add2 function takes any given input value and adds 2 to it
* We can retrieve the returned value by assigning it into a variable at the time when we call the function

---

# JS Arrays

* Arrays are a way of storing data in a sequence
* TODO

---

# JS Map

* TODO

---

# JS Objects

* TODO

---

# JS Conditionals - If Statements & Ternary Operator

* TODO

---

# JSX Introduction

* JSX (JavaScript XML) is a powerful syntax extension for JavaScript
* JSX fuses markup with Javascript, allowing you to co-locate logic and layout 
* This technique reduces a lot of the boilerplate of other templating systems
* JSX allows developers to write UI components using familiar HTML-like syntax, making it easier to visualize and understand the structure of the UI
* JSX is the glue that holds all React and React Native applications together 
* You will spend much of your time writing JSX

---

# JSX Expressions

* One of the key benefits of JSX is its ability to seamlessly integrate JavaScript expressions and logic within the markup 
* This means that you can embed variables, functions, and conditional statements directly within your JSX code 
* For example, you can use JavaScript expressions within curly braces {} to dynamically generate content
<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-jsx-expressions?iframeId=w8qg3lmdi9&amp;preview=true&amp;platform=web&amp;theme=light" height="280px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>
* See how the Text element displays the contents of the variable “value”? 
* That’s because the curly braces { } make React evaluate the expression {in between} them, returning the result of expression - in this case, the string stored in the variable “value”

---

# Writing Custom Components 

* Components are a way of packaging and reusing code - write once, use repeatedly! 
* We’ve already seen a handful of common component examples - Text, View & Image 
* These components can be used as building blocks for our own custom components
* Components are defined as JS Functions that return JSX markup
<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-hello-world-component?iframeId=ruov19et0x&amp;preview=true&amp;platform=web&amp;theme=light" height="400px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>
* Here we define two components, A and B, one shows Text and the other shows an Image
* In the App component we place A and B, notice how we just need the name of the component and all its details are rendered for us

---

# Component Props

* Props (properties) are a means of relaying information from one component to another
* Component Props are similar to Function parameters
* To declare props, use curly braces inside the component function's parameter list:
<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-props-example?iframeId=i59wyr3ii3&amp;preview=true&amp;platform=web&amp;theme=light" height="400px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>
* Here we define the CustomText component, which accepts “title” as a prop, which it then places in its styled Text component
* See how we reused one component but got three different results!

---

# Course Communication - ShiftKey Discord

![](./images/sk-discord.png)

---

# 10 min break

---

# State 

* State allows components to keep track of changing data and re-render based on changes to the data
* Some examples:
	* The color of a Text component
	* Whether or not a checkbox is checked
	* The number stored in a variable
* Want your app to be more dynamic? You probably need to make use of State

---

# Hooks

* State is implemented in React Native using Hooks
* Specifically, the simplest one is: useState
* Whenever you see the prefix "use", it's referring to a React Hook - a way of integrating functionality into components
* Hooks have a specific set of rules of when they can and can't be used - more on that later

---

# useState

* useState is a simple and effective way to manage state in your app
```js
const [value, setValue] = useState(0);
setValue(10); // this will cause React Native to re-render and all references to value to become 10
```
* When you call it, it gives you back a variable (the name of which you pick) and a function to set that variable
* React knows to re-render when the variable changes

---

# TouchableOpacity

* TouchableOpacity is the simplest way to create fully customizable buttons in React Native
* Note that there’s also a Button component, but it’s very limited in how you can style it
* TouchableOpacity is more like a View in that it doesn’t render anything by default - instead you customize it's background and give it child components to render
* There’s an opacity animation applied on press to the component
* There's an onPress prop to which you pass a callback function

---

# TouchableOpacity x useState - Toggle

<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-touchableopacity?iframeId=612tk1vj7x&amp;preview=true&amp;platform=web&amp;theme=light" height="450px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# TextInput x useState - Text Data Input

* **TextInput** is the primary method for entering text in RN. Here are some of its useful props:
* The **placeholder** prop which lets you set initial text that disappears when user types something in
* The **onChangeText** prop which accepts a callback function to invoke when the TextInput’s value changes - usually used to store the data
* The **value** prop which accepts a value the TextInput should be displayed - this can be a variable storing the data of the TextInput, usually updated by onChangeText
<iframe src="https://snack.expo.dev/embedded/@alavell/react-native-textinput?iframeId=8bruqckms3&amp;preview=true&amp;platform=web&amp;theme=light" height="400px" width="100%" frameborder="0" data-snack-iframe="true" style="display: block;"></iframe>

---

# Git Introduction

* Git is like a Time Machine for your code - it tracks changes to files over time and helps you merge conflicts
* Git was released in April 2005 - authored by Linus Torvalds, creator of Linux, and is still widely used today
* In this course you will need to use Git to manage your project app
* Git can be used on the command line as well as with graphical tools
* We'll be demonstrating git with the use of a graphical tool, Git Fork (https://git-fork.com)

---

# Git Repositories

* Git works using the concept of a **repository**
* A repository is essentially a database that tracks changes & authorship of files over time
* Repositories are stored in a hidden folder, called .git - this is created when you **initialize** a repository
* In order to interact with a repository, you issue git commands, like **git add** and **git commit** which modify the repo
* Git repositories are self-contained - i.e. they store full git history 
* Git repositories can be synchronized by using commands like **git push** and **git pull**

---

# Git - Staging & Committing Files

* In order for Git to keep track of changes, you need to explicitly tell it what changes are relevant
* When you make a change to a file in a git repository, the change will show up as **Unstaged**
* This is in reference to the **Staging Area**, which reflects Git's knowledge of upcoming changes
* When you've made a change you want to **commit** to the repository, you **add** it to the Staging Area
* Once you've added all the relevant changes to Staging, you can write a comment describing the changes and commit them
* Commiting changes makes a **Git Commit** which is a unique point in time that represents the changes since the last commit
* Collectively, a sequence of commits makes up the history that leads to the state of the repository at a given point
* Git Commits have unique SHA hashes identifying them

---

# Git Init, Stage & Commit Demo

---

# Git Branches

* You'll notice in Fork's "all commits" page there's a red box called "master"
* This is the name given to the default **branch** in git
* A branch represents a sequence of commits and is useful for segmenting git history
* You can have a number of branches, all with different names & representing different aspects of git history
* Branches can be **merged** into one another, allowing git histories which have diverged to converge
* It's common practice to have a main branch, and to create new branches that store history for new features you're implementing
* When the new feature is complete, you can merge the branch back into mainline

---

# Git Branching Demo

---

# Github, Git Remotes & Git Push/Pull

* Github is a cloud service owned by Microsoft that stores Git repositories for users & organizations
* Git is *not* Github (folks often get them mixed up)
* Github provides a ton of tooling on top of Git that makes it even easier to use
* You setup a Git repository on Github, and you set one up locally, and you store a link to the Github repository as a **Remote** in Git
* Once you've linked the repos in this way, you can **push** and **pull** git commmits to and from git branches - this is what synchronizes the repos

---

# Github Setup Demo

---

# Course Project - SKNotes App

* Local-only (no data in the cloud) note-taking app with interface inspired by Google Keep
* Testflight (iOS) and Google Play (Android) links posted in the Discord to download the reference app   
* Starter React Native project Github link posted in Discord

---


# Cloning the Git Repository

* 

---