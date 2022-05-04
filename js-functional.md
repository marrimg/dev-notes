# Functional Javascript

https://blog.bitsrc.io/understanding-currying-in-javascript-ceb2188c339

Functional programming is a style of programming that attempts to pass functions as arguments(callbacks) and return functions without side-effects(changes to the program’s state).

https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0
Haskell and other functional languages frequently isolate and encapsulate side effects from pure functions using monads. The topic of monads is deep enough to write a book on, so we’ll save that for later.

What you do need to know right now is that side-effect actions need to be isolated from the rest of your software. If you keep your side effects separate from the rest of your program logic, your software will be much easier to extend, refactor, debug, test, and maintain.

## Functional programming is a declarative paradigm, meaning that the program logic is expressed without explicitly describing the flow control.

Imperative programs spend lines of code describing the specific steps used to achieve the desired results — the flow control: How to do things.

Declarative programs abstract the flow control process, and instead spend lines of code describing the data flow: What to do. The how gets abstracted away.

## Closures

https://medium.com/@rlynjb/js-interview-question-what-is-a-closure-and-how-why-would-you-use-one-b6fd45ea95f6
Closures are inner functions inside of an outer function. They have their own local scope and has access to outer function’s scope, parameters (but NOT arguments object), and they also have access to global variables.

https://medium.com/javascript-scene/master-the-javascript-interview-what-is-a-closure-b2f0d2152b36
A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function’s scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

In JavaScript, closures are the primary mechanism used to enable data privacy. When you use closures for data privacy, the enclosed variables are only in scope within the containing (outer) function. You can’t get at the data from an outside scope except through the object’s privileged methods. In JavaScript, any exposed method defined within the closure scope is privileged. For example:

Objects are not the only way to produce data privacy. Closures can also be used to create stateful functions whose return values may be influenced by their internal state, e.g.:

const secret = msg => () => msg;

# Partial application

The idea is as follows: If you don’t provide all parameters for a function, it returns a function whose input are the remaining parameters and whose output is the result of the original function.

# Currying

https://codeburst.io/currying-in-javascript-ba51eb9778dc

Currying is a technique of evaluating function with multiple arguments, into sequence of function with single argument.

Why it’s useful ?

Currying helps you to avoid passing the same variable again and again.
It helps to create a higher order function. It extremely helpful in event handling. See the blog post for more information.
Little pieces can be configured and reused with ease.

https://medium.com/javascript-scene/curry-and-function-composition-2c208d774983

Partial applications can take as many or as few arguments a time as desired. Curried functions on the other hand always return a unary function: a function which takes one argument.

We can write a function to compose as many functions as you like. In other words, compose() creates a pipeline of functions with the output of one function connected to the input of the next.

https://www.sitepoint.com/currying-in-functional-javascript/

Our First Curry

```
var greetCurried = function(greeting) {
  return function(name) {
    console.log(greeting + ", " + name);
  };
};
```

This tiny adjustment to the way we wrote the function lets us create a new function for any type of greeting, and pass that new function the name of the person that we want to greet:

```
var greetHello = greetCurried("Hello");
greetHello("Heidi"); //"Hello, Heidi"
greetHello("Eddie"); //"Hello, Eddie"
We can also call the original curried function directly, just by passing each of the parameters in a separate set of parentheses, one right after the other:

greetCurried("Hi there")("Howard"); //"Hi there, Howard"
```

Why not try this out in your browser?

Currying is an incredibly useful technique from functional JavaScript. It allows you to generate a library of small, easily configured functions that behave consistently, are quick to use, and that can be understood when reading your code. Adding currying to your coding practice will encourage the use of partially applied functions throughout your code, avoiding a lot of potential repetition, and may help get you into better habits about naming and dealing with function arguments.
