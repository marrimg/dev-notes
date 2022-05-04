# Login/authentication

https://stackoverflow.com/questions/47122923/how-to-send-password-in-encrypted-form-from-reactjs-to-expressjs

You don't need to encrypt the password in the frontend before sending it to the backend as far as you are using an HTTPS connection and sending it as form parameters. However, you should not store the password in the browser local storage, you could ask your backend a connection token that you will store as the session identifier.

# Hoisting

https://www.sitepoint.com/back-to-basics-javascript-hoisting/

This is truly interesting behavior. To understand what’s going on here, you have to understand hoisting. Hoisting is the JavaScript interpreter’s action of moving all variable and function declarations to the top of the current scope. However, only the actual declarations are hoisted. Any assignments are left where they are. Therefore, our second example IIFE actually translates to the following code.

```
(function() {
  var foo;
  var bar;
  var baz;

  foo = 1;
  alert(foo + " " + bar + " " + baz);
  bar = 2;
  baz = 3;
})();
```

As previously mentioned, function declarations are also hoisted. However, functions that are assigned to variables are not hoisted. For example, the following code will work as expected due to function declaration hoisting.

```
foo();

function foo() {
  alert("Hello!");
}
```

However, the following example will fail spectacularly. The variable declaration for foo is hoisted before the function call. However, since the assignment to foo is not hoisted, an exception is thrown for trying to call a non-function variable.

```
foo();

var foo = function() {
  alert("Hello!");
};
```

# Function declarations vs. function expressions

Explain the differences on the usage of foo between function foo() {} and var foo = function() {}
https://stackoverflow.com/questions/5403121/whats-the-difference-between-function-foo-and-foo-function

No, they're not the same, although they do both result in a function you can call via the symbol foo. One is a function declaration, the other is a function expression. They are evaluated at different times, have different effects on the scope in which they're defined, and are legal in different places.

JavaScript has two different but related things: Function declarations, and function expressions. There are marked differences between them:

This is a function declaration:

function foo() {
// ...
}
Function declarations are evaluated upon entry into the enclosing scope, before any step-by-step code is executed. The function's name (foo) is added to the enclosing scope (technically, the variable object for the execution context the function is defined in).

This is a function expression (specifically, an anonymous one, like your quoted code):

var foo = function() {
// ...
};
Function expressions are evaluated as part of the step-by-step code, at the point where they appear (just like any other expression). That one creates a function with no name, which it assigns to the foo variable.

https://medium.com/@nupoor_neha/javascript-front-end-interview-questions-1cbc5e32792b

# Call

The call() method calls a function with a given this value and arguments provided individually.

```
function Product(name, price) {
  this.name = name;
  this.price = price;
}

function Food(name, price) {
  Product.call(this, name, price);
  this.category = 'food';
}

console.log(new Food('cheese', 5).name);
// expected output: "cheese"
```

# Apply

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/apply
The apply() method calls a function with a given this value, and arguments provided as an array (or an array-like object).

# Hoisting

Explain “hoisting”
Hoisting is when a JS declaration is lifted (“hoisted”) to the top of it’s scope by the JS interpreter. What this really means is that a variable or function isn’t necessarily declared where you think it is. Understandably, this can cause problems. Variables and functions are hoisted differently, as we'll see below.

# Attribute vs. property

https://lucybain.com/blog/2014/attribute-vs-property/
JS DOM objects have properties. These properties are kind of like instance variables for the particular element. As such, a property can be different types (boolean, string, etc.). Properties can be accessed using jQuery’s prop method (as seen below) and also by interacting with the object in vanilla JS.

Attributes are in the HTML itself, rather than in the DOM. They are very similar to properties, but not quite as good. When a property is available it’s recommended that you work with properties rather than attributes.

# Same origin policy

https://www.quora.com/Explain-the-same-origin-policy-with-regards-to-JavaScript
The same origin policy states that a web browser permits script contained in one page (or frame) to access data in another page (or frame) only if both the pages have the same origin. By same origin, it means that both the pages should have been generated from same domain or sub domain. This is to prevent theft of data.

# Mutable vs. immutable

https://developer.mozilla.org/en-US/docs/Glossary/Mutable
Mutable is a type of variable that can be changed. In JavaScript, only objects and arrays are mutable, not primitive values.
(You can make a variable name point to a new value, but the previous value is still held in memory. Hence the need for garbage collection.)

# Higher-order functions

A higher-order function is a function that can take another function as an argument, or that returns a function as a result.

# Thunk

A thunk is just a nullary function – they have a variety of common uses cases, but most commonly are used to delay the evaluation of a specific computation. \*
A thunk can only be considered a higher-order function if it returns a function.
https://seanlin0800.gitbooks.io/async-performance/content/source/ch4/thunks.html
In general computer science, there's an old pre-JS concept called a "thunk." Without getting bogged down in the historical nature, a narrow expression of a thunk in JS is a function that -- without any parameters -- is wired to call another function.
In other words, you wrap a function definition around function call -- with any parameters it needs -- to defer the execution of that call, and that wrapping function is a thunk. When you later execute the thunk, you end up calling the original function.
For example:
function foo(x,y) {
return x + y;
}

function fooThunk() {
return foo( 3, 4 );
}

// later

console.log( fooThunk() ); // 7

So, a synchronous thunk is pretty straightforward. But what about an async thunk? We can essentially extend the narrow thunk definition to include it receiving a callback.
Consider:
function foo(x,y,cb) {
setTimeout( function(){
cb( x + y );
}, 1000 );
}

function fooThunk(cb) {
foo( 3, 4, cb );
}

// later

fooThunk( function(sum){
console.log( sum ); // 7
} );

https://medium.com/fullstack-academy/thunks-in-redux-the-basics-85e538a3fe60

# Nullary function

https://en.wikipedia.org/wiki/Arity#Nullary
(Dumb definition) A function that doesn’t take any arguments

# Closure

https://medium.com/dailyjs/i-never-understood-javascript-closures-9663703368e8
Here is how it works. Whenever you declare a new function and assign it to a variable, you store the function definition, as well as a closure. The closure contains all the variables that are in scope at the time of creation of the function. It is analogous to a backpack. A function definition comes with a little backpack. And in its pack it stores all the variables that were in scope at the time that the function definition was created.

https://stackoverflow.com/questions/36636/what-is-a-closure
Normally when a function exits, all its local variables are blown away. However, if we return the inner function and assign it to a variable fnc so that it persists after outer has exited, all of the variables that were in scope when inner was defined also persist. The variable a has been closed over -- it is within a closure.
Note that the variable a is totally private to fnc. This is a way of creating private variables in a functional programming language such as JavaScript.
As you might be able to guess, when I call fnc() it prints the value of a, which is "1".
https://medium.freecodecamp.org/from-reduce-to-redux-understanding-redux-by-building-redux-918ef08abafe

# Partial Application

https://medium.com/dailyjs/i-never-understood-javascript-closures-9663703368e8
Sometimes closures show up when you don’t even notice it. You may have seen an example of what we call partial application. Like in the following code.
let c = 4
const addX = x => n => n + x
const addThree = addX(3)
let d = addThree(c)
console.log('example partial application', d)
We declare a generic adder function addX that takes one parameter (x) and returns another function.
The returned function also takes one parameter and adds it to the variable x.
The variable x is part of the closure. When the variable addThree gets declared in the local context, it is assigned a function definition and a closure. The closure contains the variable x.
So now when addThree is called and executed, it has access to the variable xfrom its closure and the variable n which was passed as an argument and is able to return the sum.
In this example the console will print the number 7.

# Currying

https://hackernoon.com/ingredients-of-effective-functional-javascript-closures-partial-application-and-currying-66afe055102a
A curried function is a function that you apply 1 parameter at a time.
function partialFunctionalMap(fn) {
return function(list) {
return functionalMap(fn, list);
}
}
partialFunctionalMap is curried. In the event handler example partialHandleLinkClick isn’t, since the first application provided 2 parameters.
We could rewrite it though.
function curriedHandleLinkClick(type){
return function(activeType) {
return function(e) {
const hasKeyboardModifier = e.ctrlKey || e.shiftKey || e.altKey || e.metaKey;
updateType(type, activeType, hasKeyboardModifier);
};
};
}
And we would use this.curriedHandleLinkClick(type)(this.props.activeType) instead of this.partialHandleLinkClick(type, this.props.activeType).
This isn’t as pretty in JavaScript as in other languages since we’re replacing (arg1, arg2, arg3) with (arg1)(arg2)(arg3).

https://blog.bitsrc.io/understanding-currying-in-javascript-ceb2188c339
Currying is a process in functional programming in which we can transform a function with multiple arguments into a sequence of nesting functions. It returns a new function that expects the next argument inline.

It keeps returning a new function (that expects the current argument, like we said earlier) until all the arguments are exhausted. The arguments are kept "alive"(via closure) and all are used in execution when the final function in the currying chain is returned and executed.

## The idea behind currying is to take a function and derive a function that returns specialized function(s).

We just defined a specialized function that calculates a volume of any cylinder of length (l), 70.

It expects 3 arguments and has 2 nested functions, unlike our previous version that expects 3 arguments and has 3nesting functions.

This version isn’t a curry. We just did a partial application of the volume function.

Currying and Partial Application are related, but they are of different concepts.

Partial application transforms a function into another function with smaller arity.

Currying creates nesting functions according to the number of the arguments of the function. Each function receives an argument. If there is no argument there is no currying.

# Lambda

In computer programming, an anonymous function (function literal, lambda abstraction, or lambda expression) is a function definition that is not bound to an identifier.

# Execution Context

https://medium.com/dailyjs/i-never-understood-javascript-closures-9663703368e8
In other words, as we start the program, we start in the global execution context. Some variables are declared within the global execution context. We call these global variables. When the program calls a function, what happens? A few steps:
JavaScript creates a new execution context, a local execution context
That local execution context will have its own set of variables, these variables will be local to that execution context.
The new execution context is thrown onto the execution stack. Think of the execution stack as a mechanism to keep track of where the program is in its execution
When does the function end

https://hackernoon.com/execution-context-in-javascript-319dd72e8e2c
Execution context (EC) is defined as the environment in which JavaScript code is executed. By environment I mean the value of this, variables, objects, and functions JavaScript code has access to, constitutes it’s environment.

Global execution context (GEC): This is the default execution context in which JS code start it’s execution when the file first loads in the browser. All the global code are executed inside global execution context. In the browser context, if the code is executing in strict mode value of this is undefined else it is window object. Global execution context cannot be more than one because only one global environment is possible for JS code execution.

Functional execution context (FEC): Functional execution context is defined as the context created by the execution of code inside a function. Each function has it’s own execution context. It can be more than one. Functional execution context have access to all the code of global execution context. While executing global execution context code, if JS engine finds a function call, it creates a new functional execution context for that function.

Execution context stack (ECS): Execution context stack is a stack data structure to store all the execution stacks created while executing the JS code. Global execution context is present by default in execution context stack and it is at the bottom of the stack. While executing global execution context code, if JS engines finds a function call, it creates functional execution context of that function and pushes that function execution context on top of execution context stack. JS engine executes the function whose execution context is at the top of the execution context stack. Once all the code of the function is executed, JS engines pop’s out that function’s execution context and start’s executing the function which is below it.

# Scope Chain

http://davidshariff.com/blog/javascript-scope-chain-and-closures/
From my previous post, we now know that every function has an associated execution context that contains a variable object [VO], which is composed of all the variables, functions and parameters defined inside that given local function.
The scope chain property of each execution context is simply a collection of the current context's [VO] + all parent’s lexical [VO]s.

# Bound vs. unbound functions

https://stackoverflow.com/questions/24757407/bound-vs-unbound-functions
I created a JSFiddle to illustrate my understanding of the difference. An unbound function is a function that is not bound to an object, so this in that function refers to the global (window) object. You can either bind a function by making it a method of an object or explicitly binding it using the .bind() method. I demonstrated the different cases in my code:
// A function not bound to anything. "this" is the Window (root) objectvar unboundFn = function() {
alert('unboundFn: ' + this);};
unboundFn();

// A function that is part of an object. "this" is the objectvar partOfObj = function() {
alert('partOfObj: ' + this.someProp);};var theObj = {
"someProp": 'Some property',
"theFn": partOfObj
};
theObj.theFn();

// A function that is bound using .bind(), "this" is the first parametervar boundFn = function() {
alert('boundFn: ' + this.someProp);};var boundFn = boundFn.bind(theObj);
boundFn();

# Execution context vs "context"

http://ryanmorr.com/understanding-scope-and-context-in-javascript/
This is where confusion often sets in, the term “execution context” is actually for all intents and purposes referring more to scope and not context as previously discussed. It is an unfortunate naming convention, however it is the terminology as defined by the ECMAScript specification, so we’re kinda stuck with it.

# Scope vs. "context"

http://ryanmorr.com/understanding-scope-and-context-in-javascript/
Every function invocation has both a scope and a context associated with it. Fundamentally, scope is function-based while context is object-based. In other words, scope pertains to the variable access of a function when it is invoked and is unique to each invocation. Context is always the value of the this keyword which is a reference to the object that “owns” the currently executing code.

# This

http://davidshariff.com/blog/javascript-this-keyword/
http://javascriptissexy.com/understand-javascripts-this-with-clarity-and-master-it/

# "Arguments" and array-like objects

https://shifteleven.com/articles/2007/06/28/array-like-objects-in-javascript/

# Object Literal

https://www.dyn-web.com/tutorials/object-literal/
A JavaScript object literal is a comma-separated list of name-value pairs wrapped in curly braces. Object literals encapsulate data, enclosing it in a tidy package. This minimizes the use of global variables which can cause problems when combining code.
The following demonstrates an example object literal:
var myObject = {
sProp: 'some string value',
numProp: 2,
bProp: false};

# Arrow functions

Returning Object Literals from Arrow Functions
https://blog.mariusschulz.com/2015/06/09/returning-object-literals-from-arrow-functions-in-javascript
Let's assume we want the square function to return the square of the given number as a property of an object literal. This is how we'd traditionally define the function:
var square = function(n) {
return {
square: n _ n
};
};
If you were to rewrite this function expression as an arrow function, you might be tempted to simply translate it just like we did in the previous example, like this:
let square = n => { square: n _ n };
When you call square, though, you'll notice the function doesn't work as intended. No matter which input value you pass, you'll get undefined as a return value. Why is that?
The issue with the arrow function is that the parser doesn't interpret the two braces as an object literal, but as a block statement. Within that block statement, the parser sees a label called square which belongs to the expression statement n \* n. Since there's no return statement at all, the returned value is always undefined.

What you need to do is force the parser to treat the object literal as an expression so that it's not treated as a block statement. The trick is to add
parentheses around the entire body:
let square = n => ({ square: n \* n });

Once the parser encounters the opening parenthesis, it knows from the ECMAScript grammar that an expression must follow because block statements can't be parenthesized. Therefore, it parses an object literal (which is an expression) rather than a block statement (which is not).

https://medium.com/@jochasinga/context-smuggle-with-injection-6f38e0ae478e
In ES2015 (or ES6, what’s with the naming anyway), the arrow function was introduced. With a function declared using the arrow syntax, the thiskeyword behaves lexically, or binds to whatever execution context is surrounding the function it is in. For instance,

https://blog.bitsrc.io/a-practical-guide-to-es6-arrow-functions-c16975100cf5
So in short, a lexical binding can be thought of as taking (or retrieving) values from the parent scope.

https://www.quora.com/Is-there-a-dynamic-scope-in-JavaScript
To be clear, JavaScript does not, in fact, have dynamic scope. It has lexical scope. Plain and simple. But the this mechanism is kind of like dynamic scope.

The key contrast: lexical scope is write-time, whereas dynamic scope (and this!) are runtime. Lexical scope cares where a function was declared, but dynamic scope cares where a function was called from.

Finally: this cares how a function was called, which shows how closely related the this mechanism is to the idea of dynamic scoping. To dig more into this, read the title "this & Object Prototypes".

# Scoping

http://pierrespring.com/2010/05/11/function-scope-and-lexical-scoping/
To me, Scoping is the ruleset used to lookup variable values. Especially the ones that are not declared within the current Scope. Only when you exactly know how Scoping works in your language, can you be sure about the value a variable has at any given place in your code. It is very important to understand how this is implemented in your language of choice.

Wikipedia defines Scope as follows:
Typically, scope is used to define the extent of information hiding—that is, the visibility or accessibility of variables from different parts of the program.
In JavaScript we have Function Scope and Lexical Scoping. (and block scoping)
Function Scope means that any variable which is defined within a function is visible within that entire function. This is quite different form Block Scope, in which a variable scope is limited by the block a variable is declared in. A block is usually what you find between {curly braces} or loop variables.

Lexical Scoping defines how variable names are resolved in nested functions. Other names of Lexical Scoping are Static Scoping or Closure. It means that the scope of an inner function contains the scope of a parent function.
...
If you bare with me for a little more, you will know it all. There is a little more to it, and that little more is what makes Lexical Scoping so powerful: inner functions contain the scope of parent functions even if the parent function has returned.

# Lexical Scope

https://stackoverflow.com/questions/1047454/what-is-lexical-scope
Lets try the shortest possible definition:
Lexical Scoping defines how variable names are resolved in nested functions: inner functions contain the scope of parent functions even if the parent function has returned.
That's all there is to it! To help myself understand what this means, I wrote an in depth blog post about function scope and lexical scoping in JavaScript which can be found here. Maybe this could serve someone else too.

http://pierrespring.com/2010/05/11/function-scope-and-lexical-scoping/

Lexical Scoping defines how variable names are resolved in nested functions. Other names of Lexical Scoping are Static Scoping or Closure. It means that the scope of an inner function contains the scope of a parent function. Let’s have a look at the following example:

# Block Scopes

https://edgecoders.com/function-scopes-and-block-scopes-in-javascript-25bbd7f293d7?gi=22e54c207c89
https://medium.com/@josephcardillo/the-difference-between-function-and-block-scope-in-javascript-4296b2322abe
https://stackoverflow.com/questions/30705116/block-scope-function-scope-and-local-scope-in-javascript

I'm not sure you really got your questions answered yet:
Is block scope sometimes the same as function scope? I know function scope is for everything inside a function, but don't get what exactly a block scope is.
Yes, a block scope is sometimes the same as a function scope. Block scope is everything inside a set of braces { a block scope here }. So, at the top of a function's code, a block scope will be the same as a function scope:
function test(x) {
// this is both a block scope and a function scope
let y = 5;
if (x) {
// this is a smaller block scope that is not the same as the function scope
let z = 1;
}}
For Javascript, is it currently recommended to use let / const instead of var for future maintenance? (This was from Airbnb Style Guide)
let and const are part of the newest ES6 specification and are only implemented in the latest Javascript engines and sometimes in the latest engines they are only enabled with special flags. They are coming to all newer JS engines/browsers, but are not widely deployed yet. Thus, if you are writing Javascript for regular browser consumption across the broad internet, you cannot reliably use let and const yet.

# Switch statements

In JavaScript, is returning out of a switch statement considered a better practice than using break?
https://stackoverflow.com/questions/6114210/in-javascript-is-returning-out-of-a-switch-statement-considered-a-better-practi
A break will allow you continue processing in the function. Just returning out of the switch is fine if that's all you want to do in the function.

# Arrow functions and lexical "this"

https://hackernoon.com/javascript-es6-arrow-functions-and-lexical-this-f2a3e2a5e8c4
It promises a shorter syntax than it’s predecessor the Function Expression. In addition(and IMHO more exciting) is how the new Arrow Function binds, or actually DOES NOT bind it’s own this. Arrow Functions lexically bind their context so this actually refers to the originating context.
https://tylermcginnis.com/arrow-functions/

# Methods and "this"

https://blog.kevinchisholm.com/javascript/the-javascript-this-keyword-deep-dive-nested-functions/
In this article we learned that when a function is not specified as a method of an object, the JavaScript “this” keyword refers to the window object. This is true even in the case of nested functions. In fact, no matter how many levels deep we nest functions, the JavaScript “this” keyword refers to the window object.

# Classes and "this"

https://stackoverflow.com/questions/36489579/this-within-es6-class-method

https://javascript.info/class

https://stackoverflow.com/questions/3894119/variables-scope-in-a-switch-case

Async await try/catch

async function f3() {
try {
var z = await Promise.reject(30);
} catch(e) {
console.log(e); // 30
}}f3();

The word “async” before a function means one simple thing: a function always returns a promise.
(See event loop/async functions note)

# Template literals

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
Template literals are string literals allowing embedded expressions. You can use multi-line strings and string interpolation features with them. They were called "template strings" in prior editions of the ES2015 specification.

# toString vs. json.stringify

https://stackoverflow.com/questions/15834172/whats-the-difference-in-using-tostring-compared-to-json-stringify

Unless you have a custom object with custom .toString method returning JSON.stringify of that object, there is no obj that would give obj.toString() == JSON.stringify(obj).
When obj is an array like [1,2,3] then .toString() gives:
"1,2,3"
And JSON.stringify:
"[1,2,3]"
These are close but not quite the same, the JSON serialized one has no ambiguity with commas and directly runs as Javascript or can be parsed as JSON.
See:
["1,",2,3].toString();//"1,,2,3" ... so you can't just split by comma and get original array//it is in fact impossible to restore the original array from this result

JSON.stringify(["1,",2,3])//'["1,",2,3]'//original array can be restored exactly

# Inheritance

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain
When it comes to inheritance, JavaScript only has one construct: objects. Each object has a private property which holds a link to another object called its prototype. That prototype object has a prototype of its own, and so on until an object is reached with null as its prototype. By definition, null has no prototype, and acts as the final link in this prototype chain.

JavaScript objects are dynamic "bags" of properties (referred to as own properties). JavaScript objects have a link to a prototype object. When trying to access a property of an object, the property will not only be sought on the object but on the prototype of the object, the prototype of the prototype, and so on until either a property with a matching name is found or the end of the prototype chain is reached.

https://hackernoon.com/prototypes-in-javascript-5bba2990e04b

# Function declaration vs function expression

https://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/

b) Function Expressions are more versatile. A Function Declaration can only exist as a “statement” in isolation. All it can do is create an object variable parented by its current scope. In contrast a Function Expression (by definition) is part of a larger construct. If you want to create an anonymous function or assign a function to a prototype or as a property of some other object you need a Function Expression. Whenever you create a new function using a high order application such as curry or compose you are using a Function Expression. Function Expressions and Functional Programming are inseparable.

# What is a lambda expression?

Lambda expressions (or lambda functions) are essentially blocks of code that can be assigned to variables, passed as an argument, or returned from a function call, in languages that support high-order functions.

Lambda expressions are present in most of modern programming languages (Python, Ruby, Java...). They are simply expressions that create functions. This is really important for a programming language to support first-class functions which basically means passing functions as arguments to other functions or assigning them to variables.
