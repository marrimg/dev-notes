https://github.com/valerybugakov/interview-answers/tree/master/javascript
https://github.com/yangshun/front-end-interview-handbook/blob/master/questions/javascript-questions.md#what-advantage-is-there-for-using-the-arrow-syntax-for-a-method-in-a-constructor

# Explain event delegation.

Event delegation takes advantage of event bubbling to let you set an event handler on a parent HTML element that would be triggered by a click on any of its children. When you click on a nested element, the event bubbles up through that element's parent elements. So, if you put the event handler on a parent element, a click on any of its children will bubble up and get triggered. target.addEventListener()

# Explain how this works in JavaScript.

The 'this' keyword is defined after an object invokes a function. Most of the time, 'this' refers to the object that invokes the function. For example, if you define a function called 'getName' in an object called person, and invoke 'getName' by calling person.getName(), 'this' refers to the 'person' object:

```
var person = {
  name: 'Lisa',
  getName: function(){
    console.log(this.name);
  }
}
person.getName();
```

You can change the context of 'getName' by using apply, call, or bind.
If you pass a method as a callback, 'this' will refer to the object that is now invoking it, not the object it's defined in. 'This' is also only available to methods of the object itself, but not by nested functions inside them.

# Can you give an example of one of the ways that working with this has changed in ES6?

Arrow functions don't bind this; they use lexical scoping and inherit their 'this' value from their parent scope. This can make it easier to work with the this keyword -- for example, in a class component in React, if you pass an arrow function as a callback to a click handler, you don't have to worry about 'this' being bound to the object that the click handler is being called on. You don't have to bind the method to 'this' in the class constructor function to get the correct 'this' value.

# Explain how prototypal inheritance works.

Inheritance refers to an object’s ability to access methods and other properties from another object.

In JS, all functions are objects, which can have properties. Objects in JS have a property called 'prototype', which is also an object. If you call a constructor function with the 'new' keyword, it will return a new object that **has access** to the prototype of the original object through the **prototype chain**. That means that when we look for a property on the new object, JS will check the object itself, then check the object's prototype, then the prototype's prototype, and so on until it finds an object with a null prototype property.

# What's the difference between a variable that is: null, undefined or undeclared?

An undefined variable is a variable that has been declared but has not been assigned a value.
Null is an assignment value that represents no value.
An undeclared variable has not been declared using the 'var' keyword

# How would you go about checking for any of these states?

if(foo === undefined){}
if(foo === null){}

# What is a closure, and how/why would you use one?

What a closure is: When you return a function from a function, the inner function has access to variables from the outer function's scope, even though the outer function has returned. The outer function's scope can now only be accessed through the inner function.
How/why you use one: Data privacy, stateful functions, partial application, currying

```
const partialApply = (fn, ...fixedArgs) => {
  return function (...remainingArgs) {
    return fn.apply(this, fixedArgs.concat(remainingArgs));
  };
};
const add = (a, b) => a + b;

const add10 = partialApply(add, 10);
add10(5);
```

# What language constructions do you use for iterating over object properties and array items?

Object.keys(object1)
Object.values(object1)
array.map, array.reduce, array.filter, array.forEach()

# Can you describe the main difference between the Array.forEach() loop and Array.map() methods and why you would pick one versus the other?

They both perform an operation for each element in an array, but .map returns a new array with the result of the operation on each item. You would pick forEach if you don't need a new array, for example to console.log each element. You would pick map if you want a new array of items that have been transformed in some way.

# What's a typical use case for anonymous functions?

Passing it as a parameter to another function, for example, inside array.map

# What's the difference between host objects and native objects?

https://medium.com/@rlynjb/js-interview-question-what-s-the-difference-between-host-objects-and-native-objects-b395f7c5fbf1

# Explain the difference between: function Person(){}, var person = Person(), and var person = new Person()?

function Person(){} is a function declaration. It does not execute at this time.
var person = Person() is a funciton expression. It assigns the returned value of the Person() funtion to the variable person
var person = new Person() is creating a new instance of the constructor function Person and assigning it to a variable.

# Explain the differences on the usage of foo between function foo() {} and var foo = function() {}

function foo(){} is a function declaration. A function declaration is hoisted to the top of the scope. They are evaluated upon entry to the enclosing scope, before step-by-step code.
var foo = function(){} is a function expression. These are evaluated as part of the step-by-step code evaluation in the execution scope. For a function expression assigned to a variable, the variable name gets hoisted but the top, but not the function itself.

# Can you explain what Function.call and Function.apply do? What's the notable difference between the two?

call and apply are methods that allow you to call a function and pass it a context, or 'this' value. Both allow you to pass variables to the function, but apply allows you to pass the variables as an array.

# Explain Function.prototype.bind.

when you call .bind on a function with an object, it returns a new function that has its 'this' value bound to the provided object. Unlike apply and call, the function is not called.

# What's the difference between feature detection, feature inference, and using the UA string?

# Explain "hoisting".

Variable and function declarations are hoisted to the top of their scope before they are executed. Variable initializations are not hoisted, so the variable will be set to undefined until the variable is initialized later in the execution.

# Describe event bubbling.

When you click on an HTML element, a click event is triggered on the element, and then on its parent element, and so on up the DOM tree until it stops at the window object. You can stop this behavior with event.stopPropagation();

# Describe event capturing.

When you click on an HTML element, a click event is triggered on the outermost parent element in the DOM tree and propagated down to the target element. You can choose whether your event is handled first by the parent and propagated to the target, or handled first by the target and propagated to the parent. You can enable capturing by passing true as the last parameter to addEventListener(type, listener[, useCapture]) You can stop propagation with event.stopPropagation();

# What's the difference between an "attribute" and a "property"?

the HTML representation of a DOM element has attributes (that being the term used in XML for the key/value pairs contained within a tag) but when represented as a JavaScript object those attributes appear as object properties.

# What are the pros and cons of extending built-in JavaScript objects?

I would say that it's always a bad idea to extend built in objects, because it is too easy to break the default behavior of the language. For example, libraries depend on consistent default JS behavior

# What is the difference between == and ===?

They both test for equality, but the triple equals can only return true if the two things being compared are of the same type. == tries to do a type conversion, but that can lead to unexpected results.

# Explain the same-origin policy with regards to JavaScript.

the same origin policy is a browser security feature that stops code from a different domain from executing on a site. This can prevent a malicious attack from outside the site. You can work around this by, for example, allowing CORS on your server, which will return a Access-Control-Allow-Origin header.

# Why is it called a Ternary operator, what does the word "Ternary" indicate?

A ternary is a one line shorthand for an if-then statement. It has three parts: the statement, if true, and if false

# What is strict mode? What are some of the advantages/disadvantages of using it?

JS behaves differently in strict mode. Strict mode eliminates silent errors. The 'this' keyword is undefined unless explicitly bound -- in non-strict mode, it defaults to the window/global object.

# What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?

Advantages = you can get features that the language does not have on its own, like static typing if you use TypeScript.
Disadvantages = extra steps to compile, adds complexity to project, possible learning curve for new devs

# What tools and techniques do you use debugging JavaScript code?

debugger statement, breakpoints in chrome dev tools, React developer tools, Redux developer tools, network tab to check if request was sent

# Explain the difference between mutable and immutable objects.

Mutable: the object can be changed once created
Immutable: the object cannot be changed once created

# What is an example of an immutable object in JavaScript?

Numbers, strings, Object.freeze(), immutable.js, discipline (don't mutate Redux state etc)

# What are the pros and cons of immutability?

# How can you achieve immutability in your own code?

Object.freeze(), discipline (don't mutate Redux state, use spread operator instead of concat, ect)

# Explain the difference between synchronous and asynchronous functions.

Synchronous functions complete before the next code block is run -- they are blocking. Async functions invoke a callback function when an asynchronous operation is finished and do not block the rest of code from continuing.

# What is the event loop?

JavaScript is a single-threaded language with a single call stack that keeps track of the code that is currently being evaluated and the code that needs to be evaluated after that. The Event Loop in JS is a process that constantly checks the call stack to to see if something needs to be run.

# What is the difference between call stack and task queue?

The call stack keeps track of the code that is currently being evaluated and the code that needs to be evaluated after that. The callback queue (message queue) (event queue) is where callbacks from asynchronous browser operations (like setTimeout) wait for execution. The task queue (job queue?) stores callbacks from promises until the promise resolves, at which time the callbacks are executed immediately. Items in the task queue have a higher priority than items in the callback (message) queue.

# What are the differences between variables created using let, var or const?

let and const are block scoped (only accessible inside the nearest set of curly braces in a funciton, if-else block or loop). A const value should not be reassigned.

var declarations are hoisted, while let and const are not

# What are the differences between ES6 class and ES5 function constructors?

A class is syntactic sugar for a constructor function that makes the syntax shorter and more similar looking to "traditional" OOP. In an es6 class, you can include a constructor method, where you define object properties, and put methods in the class's body. When you put a method in an es6 class's body, this is the same as assigning a method to a constructor function's prototype.

# Can you offer a use case for the new arrow => function syntax? How does this new syntax differ from other functions?

- simplifies syntax
- lexical scoping for 'this' keyword - makes 'this' more predictible
- lambda functions

# What advantage is there for using the arrow syntax for a method in a constructor?

The main advantage of using an arrow function as a method inside a constructor is that the value of this gets set at the time of the function creation and can't change after that. So, when the constructor is used to create a new object, this will always refer to that object.

```
const Person = function(firstName) {
  this.firstName = firstName;
  this.sayName1 = function() { console.log(this.firstName); };
  this.sayName2 = () => { console.log(this.firstName); };
};

const john = new Person('John');
const dave = new Person('Dave');

john.sayName1(); // John
john.sayName2(); // John

// The regular function can have its 'this' value changed, but the arrow function cannot
john.sayName1.call(dave); // Dave (because "this" is now the dave object)
john.sayName2.call(dave); // John

```

# What is the definition of a higher-order function?

A higher-order function is a function that accepts other function as an argument or returns a function as a return value.

# Can you give an example for destructuring an object or an array?

Destructuring lets you extract data from an object or an array into its own variable, as in:

```
const person = {
  first: 'Wes',
  last: 'Bos'
}
const { first, last } = person;
```

This gives you a much easier and shorter syntax to create the variables first = 'Wes' and last = 'Bos' than if you had to assign properties from the object to the new variables manually.

# Can you give an example of generating a string with ES6 Template Literals?

Template literals are string literals allowing embedded expressions: `Hello, ${userName}`

# Can you give an example of a curry function and why this syntax offers an advantage?

A curry function is a sequence of functions that each take one argument and return the next function in the sequence

# What are the benefits of using spread syntax and how is it different from rest syntax?

Spread syntax expands iterables into an array, object or function call. You can use it to shallow clone an object (in a simpler way than object.assign) or create a new array from the items of other arrays, which avoids mutating one of your existing arrays like you would with array.concat()

Rest syntax looks exactly like spread syntax but is used for destructuring arrays and objects. In a way, rest syntax is the opposite of spread syntax: spread 'expands' an array into its elements, while rest collects multiple elements and 'condenses' them into a single element. See rest parameters.

One example of rest syntax is a function that can take any number of arguments:

```
const foo = (...args) => {
   console.log(...args);
};


foo('foo', 'bar', 'foobar')
```

# How can you share code between files?

require or export/import

# Why you might want to create static class members?

It is common to use static methods as an alternative constructor.
Moreover, they are frequently used in order to define utility and helper functions.

///

# What is a lambda expression?

A lambda expression is a function that can be passed around like data: for example, passed to or returned from another function.

# what is a first class function?

First-class type means simply, that the type can be used as a value of a variable. A string is a first-class type as well as a function is a first-class type in JavaScript and so your functions can accept other functions as their arguments and return functions as their return values.

# What is a pure function?

A pure function is a function where the return value is only determined by its arguments without any side effects.

# What is the imperative paradigm?

Procedural and object-oriented programming belong under imperative paradigm that you know from languages like C, C++, C#, PHP, Java and of course Assembly.

Your code focuses on creating statements that change program states by creating algorithms that tell the computer how to do things. It closely relates to how hardware works. Typically your code will make use of conditinal statements, loops and class inheritence.

# What is the declarative paradigm?

Declarative code focuses on building logic of software without actually describing its flow. You are saying what without adding how. For example with HTML you use <img src="./image.jpg" /> to tell browser to display an image and you don’t care how it does that.
Functional programming based on lambda calculus is Turing complete, avoids states, side effects and mutation of data. You create expressions instead of statements and evaluate functions. You don’t have any use for loops and for the same argument your function will always return the same value.
Example of declarative code in JavaScript:
const sum = a => b => a + b;
console.log (sum (5) (3)); // 8

# What is an expression? What is a statement?

An expression is any valid unit of code that resolves to a value.
A statement is (roughly) an instruction, an action.
if, while, for, const are examples of statements. They perform actions or control actions, but don't resolve to values.

# React lifecycle

https://blog.bitsrc.io/react-16-lifecycle-methods-how-and-when-to-use-them-f4ad31fb2282

## Mounting

Constructor (class only)
getDerivedStateFromProps
render
componentDidMount

## Updating

getDerivedStateFromProps
shouldComponentUpdate
getSnapshotBeforeUpdate
componentDidUpdate

# Unmounting

componentWillUnmount

## DEPRECATED

https://levelup.gitconnected.com/componentdidmakesense-react-lifecycle-explanation-393dcb19e459

https://hackernoon.com/problematic-react-lifecycle-methods-are-going-away-in-react-17-4216acc7d58b

Why did they decide to get rid of them? The original lifecycle model was not intended for some of the upcoming features like async rendering. With the introduction of async rendering, some of these lifecycle methods will be unsafe if used.

Legacy lifecycle

componentWillMount
componentWillRecieveProps
componentWillUpdate

# React Hooks

With Hooks, we can create functional components that uses state and lifecycle methods.

https://reactjs.org/docs/hooks-overview.html

## useState

## useEffect

When you call useEffect, you’re telling React to run your “effect” function after flushing changes to the DOM. Effects are declared inside the component so they have access to its props and state. By default, React runs the effects after every render — including the first render. (We’ll talk more about how this compares to class lifecycles in Using the Effect Hook.)

https://medium.com/codingthesmartway-com-blog/react-hooks-explained-functional-components-with-state-122cc7faf770

# Refs in React

https://reactjs.org/docs/refs-and-the-dom.html
When the ref attribute is used on an HTML element, the ref created in the constructor with React.createRef() receives the underlying DOM element as its current property

When a ref is passed to an element in render, a reference to the node becomes accessible at the current attribute of the ref.

When the ref attribute is used on a custom class component, the ref object receives the mounted instance of the component as its current.
You may not use the ref attribute on function components because they don’t have instances.

# Semantic HTML and ARIA

https://css-tricks.com/why-how-and-when-to-use-semantic-html-and-aria/
Combine ARIA with semantic HTML to support screen readers

# Cookies vs. Local Storage

https://medium.com/swlh/cookies-vs-localstorage-whats-the-difference-d99f0eb09b44
While these storage options have their positives and negatives, they both have applications in modern web development. Cookies are smaller and send server information back with every HTTP request, while LocalStorage is larger and can hold information on the client side.

https://thoughtbot.com/blog/lucky-cookies

https://stackoverflow.com/questions/1336126/does-every-web-request-send-the-browser-cookies

# What is the DOM?

https://www.digitalocean.com/community/tutorials/introduction-to-the-dom
In addition to parsing the style and structure of the HTML and CSS, the browser creates a representation of the document known as the Document Object Model. This model allows JavaScript to access the text content and elements of the website document as objects.

# How do browsers render web pages?
https://blog.logrocket.com/how-browser-rendering-works-behind-the-scenes-6782b0e8fb10/
The browser engine figures out what to display to users based on the files it receives.
The browser receives data as packets of [raw bytes](https://softwareengineering.stackexchange.com/questions/216597/what-is-a-byte-stream-actually/216600).
The browser converts the raw bytes of data into a format it understands.
The browser needs a DOM object. It converts the byte data into characters, and then again into *tokens*.
When you save a file with the .html extension, you tell the browser engine to interpret the file as an html document. The parser understands html tags and the rules that apply to them.
Tokens are small data structures that contain information about the tags in the document.
The tokens are then converted into nodes, which are linked into a tree data structure known as the DOM.
The DOM establishes parent-child relationships between the nodes and creates the DOM tree.
Meanwhile, the browser goes through a similar process with the CSS to create a CSSDOM tree. The CSSDOM tree establishes a heirarchy of styles (the cascade).
Now, the browser has two trees: the DOM and the CSSDOM.
Next, it combines both trees into a *render tree*
If an element has been hidden using `display:none;`, it will be included in the DOM but not the render tree.
With the render tree constructed, the browser performs the layout.

## Render Blocking

When you hear render blocking, what comes to mind? Well, my guess is, “Something that prevents the actual painting of nodes on the screen’.”

If you said that, you’re absolutely right!

The first rule for optimizing your website is to get the most important HTML and CSS delivered to the client as fast as possible. The DOM and CSSOM must be constructed before a successful paint, so both HTML and CSS are render blocking resources.

## JavaScript
What happens to this flow once we introduce JavaScript? Well, one of the most important things to remember is that whenever the browser encounters a script tag, the DOM construction is paused! The entire DOM construction process is halted until the script finishes executing.

The point is, you should get your HTML and CSS to the client as soon as possible to optimize the time to the first render of your applications.

---

—
Amazon Aurora
RELATIONAL DATABASE, SIMILAR TO POSTGRES

Amazon DynamoDB
NON-RELATIONAL DATABASE
tools team
customizaion
tool team
interfaces that create the data for customization

# JS Interview Questions

## Double vs triple equal

The triple equals operator (===) returns true if both operands are of the same type and contain the same value. If comparing different types for equality, the result is false.

The double equals operator (==) tries to perform type conversion if the types differ and then compare for equality. If the types differ, either or both operands are first converted to a common type. The conversion rules are complex and depend on the argument types. For a full comparison table, see for example MDN or the ECMAScript specification.

## Target a DOM element (vanilla)

var el = document.getElementById('foo');
el.innerHTML = 'Hello World!';

## Event bubbling

https://javascript.info/bubbling-and-capturing

The bubbling principle is simple.

When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors.

A bubbling event goes from the target element straight up. Normally it goes upwards till <html>, and then to document object, and some events even reach window, calling all handlers on the path.

But any handler may decide that the event has been fully processed and stop the bubbling.

The method for it is event.stopPropagation().

For instance, here body.onclick doesn’t work if you click on <button>:

```
 <body onclick="alert(`the bubbling doesn't reach here`)">
  <button onclick="event.stopPropagation()">Click me</button>
</body>
```

# JS DOM methods

https://www.freecodecamp.org/news/whats-the-document-object-model-and-why-you-should-know-how-to-use-it-1a2d0bc5429d/
The DOM (Document Object Model) is an interface that represents how your HTML and XML documents are read by the browser.

https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction

The following is a brief list of common APIs in web and XML page scripting using the DOM.

document.getElementById(id)
document.getElementsByTagName(name)
document.createElement(name)
parentNode.appendChild(node)
element.innerHTML
element.style.left
element.setAttribute()
element.getAttribute()
element.addEventListener()
window.content
window.onload
console.log()
window.scrollTo()

## Document

https://developer.mozilla.org/en-US/docs/Web/API/Document

The Document interface represents any web page loaded in the browser and serves as an entry point into the web page's content, which is the DOM tree. The DOM tree includes elements such as <body> and <table>, among many others. It provides functionality globally to the document, like how to obtain the page's URL and create new elements in the document.

document.getElementById(id)
document.getElementsByTagName(name)
document.createElement(name)

https://developers.google.com/web/fundamentals/performance/critical-rendering-path/constructing-the-object-model
Conversion: The browser reads the raw bytes of HTML off the disk or network, and translates them to individual characters based on specified encoding of the file (for example, UTF-8).
Tokenizing: The browser converts strings of characters into distinct tokens—as specified by the W3C HTML5 standard; for example, "<html>", "<body>"—and other strings within angle brackets. Each token has a special meaning and its own set of rules.
Lexing: The emitted tokens are converted into "objects," which define their properties and rules.
DOM construction: Finally, because the HTML markup defines relationships between different tags (some tags are contained within other tags) the created objects are linked in a tree data structure that also captures the parent-child relationships defined in the original markup: the HTML object is a parent of the body object, the body is a parent of the paragraph object, and so on.

## Element

element.innerHTML
element.style.left
element.setAttribute()
element.getAttribute()
element.addEventListener()

## Window

window.content
window.onload
window.location
window.scrollTo()

## Console

The Console method log() outputs a message to the web console. The message may be a single string (with optional substitution values), or it may be any one or more JavaScript objects.

console.log()

STUDY:

- prototypal inheritance
- factories
- constructor functions
- composition
- Object.create() vs {}

READ:
https://medium.com/dailyjs/i-never-understood-javascript-closures-9663703368e8
https://flaviocopes.com/javascript-event-loop/

https://github.com/h5bp/Front-end-Developer-Interview-Questions/blob/master/src/questions/javascript-questions.md
https://github.com/yangshun/front-end-interview-handbook/blob/master/questions/javascript-questions.md







