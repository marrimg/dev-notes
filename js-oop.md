# Object Oriented Programming

## Prototypal Inheritance

https://medium.com/javascript-scene/master-the-javascript-interview-what-s-the-difference-between-class-prototypal-inheritance-e4cd0a7562e9

### Class inheritance vs prototypal inheritance

Class Inheritance: A class is like a blueprint — a description of the object to be created. Classes inherit from classes and create subclass relationships: hierarchical class taxonomies.

Class inheritance creates parent/child object taxonomies as a side-effect.

Prototypal Inheritance: A prototype is a working object instance. Objects inherit directly from other objects.

Prototype delegation: In JavaScript, an object may have a link to a prototype for delegation. If a property is not found on the object, the lookup is delegated to the delegate prototype, which may have a link to its own delegate prototype, and so on up the chain until you arrive at `Object.prototype`, which is the root delegate. This is the prototype that gets hooked up when you attach to a `Constructor.prototype` and instantiate with `new`. You can also use `Object.create()` for this purpose, and even mix this technique with concatenation in order to flatten multiple prototypes to a single delegate, or extend the object instance after creation.

Functional inheritance: In JavaScript, any function can create an object. When that function is not a constructor (or `class`), it’s called a factory function. Functional inheritance works by producing an object from a factory, and extending the produced object by assigning properties to it directly (using concatenative inheritance). Douglas Crockford coined the term, but functional inheritance has been in common use in JavaScript for a long time.

https://medium.com/@kevincennis/prototypal-inheritance-781bccc97edb

Here’s a fun fact: In JavaScript, all functions are also objects, which means that they can have properties. And as it so happens, they all have a property called `prototype`, which is also an object.

```
function foo() {
}
typeof foo.prototype // ‘object’
```

That’s pretty simple, right? Any time you create a function, it will automatically have a property called prototype, which will be initialized to an empty object.

Top highlight
Prototypal Inheritance in JavaScript
Kevin Ennis
Kevin Ennis
Follow
May 20, 2016 · 7 min read
Last year I wrote a post called “How to impress me in an interview”, and in it, I mentioned that I run across a lot of candidates (the vast majority, actually) who don’t really understand how prototypes work.
In a way, that’s kind of an amazing testament to how flexible JavaScript is, and how user-friendly many of today’s popular libraries are. I can’t think of many other object-oriented languages where an engineer can be reasonably productive without being at least vaguely aware of classes.
But here’s the thing: if you write JavaScript even semi-regularly, you really should understand how prototypal inheritance works. And that’s why I’m writing this post.
Disclaimer
There will be some things in this article that I over-simplify a little bit.
My goal here is to help someone who’s never used prototypal inheritance to become comfortable with it. In order to do that, I’ll cut a few small corners here and there if I think it helps eliminate a bit of confusion.
Objects Inherit from Objects
If you’ve ever read anything about inheritance in JS, then you’ve almost certainly heard that objects inherit from other objects.
This is true, and once you already understand it, it’s a good way to think about things. But my experience has been that this explanation alone isn’t really sufficient.
So I’m going to break from tradition here and not actually try to explain how inheritance works right up front. Instead, we’ll start with some simpler stuff that will hopefully provide a bit of context later on.
Function prototypes
Here’s a fun fact: In JavaScript, all functions are also objects, which means that they can have properties. And as it so happens, they all have a property called `prototype`, which is also an object.
function foo() {
}
typeof foo.prototype // ‘object’
That’s pretty simple, right? Any time you create a function, it will automatically have a property called prototype, which will be initialized to an empty object.
Constructors
In JavaScript, there’s really no difference between a “regular” function and a constructor function. They’re actually all the same. But as a convention, functions that are meant to be used as constructors are generally capitalized.
By the way, if you don’t know what I mean when I say “constructor”, that’s totally okay. We’ll get there.
So let’s say that we want to make a constructor function called Dog, because explaining inheritance using animals is a time-honored tradition and I’m kind of a nostalgic dude.
function Dog() {
}

## If I want to make an instance of Dog, I use the new keyword. That’s really what I mean when I talk about constructors — I’m using the function to construct a new object. Any time you see the new keyword, it means that the following function is being used as a constructor.

JavaScript uses an inheritance model called “differential inheritance”. What that means is that methods aren’t copied from parent to child. Instead, children have an “invisible link” back to their parent object.

What actually happens when I write fido.bark() is this:

1. The JS engine looks for a property called bark on our fido object.
2. It doesn’t find one, so it looks “up the prototype chain” to fido’s parent, which is Dog.prototype.
3. It finds Dog.prototype.bark, and calls it with this bound to fido.

## That part is really important, so I’m going to repeat it:

## There’s really no such property as fido.bark. It doesn’t exist. Instead, fido has access to the bark() method on Dog.prototype because it’s an instance of Dog. This is the “invisible link” I mentioned. More commonly, it’s referred to as the “prototype chain”.

## Prototype chain

https://dev.to/codesmith_staff/explain-javascripts-prototype-chain-like-im-five-51p

## Prototype vs "this"
https://stackoverflow.com/questions/310870/use-of-prototype-vs-this-in-javascript
As others have said the first version, using "this" results in every instance of the class A having its own independent copy of function method "x". Whereas using "prototype" will mean that each instance of class A will use the same copy of method "x".


## Constructor functions

https://css-tricks.com/understanding-javascript-constructors/

Constructors are like regular functions, but we use them with the new keyword. There are two types of constructors: built-in constructors such as Array and Object, which are available automatically in the execution environment at runtime; and custom constructors, which define properties and methods for your own type of object.

A constructor is useful when you want to create multiple similar objects with the same properties and methods. It’s a convention to capitalize the name of constructors to distinguish them from regular functions. Consider the following code:

```
function Book() {
  // unfinished code
}

var myBook = new Book();
```

The last line of the code creates an instance of Book and assigns it to a variable. Although the Book constructor doesn't do anything, myBook is still an instance of it. As you can see, there is no difference between this function and regular functions except that it's called with the new keyword and the function name is capitalized.

Another way to find the type of an instance is to use the constructor property. Consider the following code fragment:

```
myBook.constructor === Book;   // true
```

The constructor property of myBook points to Book, so the strict equality operator returns true. All objects inherit a constructor property from their prototype which point to the constructor function that has created the object:

### Object literal notations are preferred to constructors

The JavaScript language has nine built-in constructors: Object(), Array(), String(), Number(), Boolean(), Date(), Function(), Error() and RegExp(). When creating values, we are free to use either object literals or constructors. However, object literals are not only easier to read but also faster to run, because they can be optimize at parse time. Thus, for simple objects it's best to stick with literals:

As you can see there's hardly any difference between object literals and constructors, and it's still possible to call methods on literals. It's because when we call a method on a literal, behind the scene JavaScript converts the literal to a temporary object so that we can use object methods for primitive values. Once the temporary object is no longer needed, JavaScript discards it.

### Using the new keyword is essential

It's important to remember to use the new keyword before all constructors. If you accidentally forget new, you will be modifying the global object instead of the newly created object. Consider the following example:

```
function Book(name, year) {
  console.log(this);
  this.name = name;
  this.year = year;
}

var myBook = Book("js book", 2014);
console.log(myBook instanceof Book);
console.log(window.name, window.year);

var myBook = new Book("js book", 2014);
console.log(myBook instanceof Book);
console.log(myBook.name, myBook.year);
```

When we call the Book constructor without new, we are in fact calling a function without a return statement and this inside the Book constructor will be equal to Window (instead of myBook). In other words, we unintentionally create two global variables which cause the code to produce unintended results. But when we call the function with new the context is switched from global (Window) to the instance, therefore this points to myBook.

Note that in strict mode this code would throw an error because strict mode is designed to protect the programmer from accidentally calling a constructor without the new keyword.

It's important to understand that the class declaration introduced in ES2015 simply works as syntactic sugar over the existing prototype-based inheritance and does not add anything new to JavaScript. Constructors and prototypes are JavaScript's primary way of defining similar and related objects.

https://www.tutorialsteacher.com/javascript/new-keyword-in-javascript

## The new keyword performs following four tasks:

### It creates new empty object e.g. obj = { };

### It sets new empty object's invisible 'prototype' property to be the constructor function's visible and accessible 'prototype' property. (Every function has visible 'prototype' property whereas every object includes invisible 'prototype' property)

### It binds property or function which is declared with this keyword to the new object.

### It returns newly created object unless the constructor function returns a non-primitive value (custom JavaScript object). If constructor function does not include return statement then compiler will insert 'return this;' implicitly at the end of the function. If the constructor function returns a primitive value then it will be ignored.

# JavaScript Factory Functions vs Constructor Functions vs Classes

https://medium.com/javascript-scene/javascript-factory-functions-vs-constructor-functions-vs-classes-2f22ceddf33e

Prior to ES6, there was a lot of confusion about the differences between a factory function and a constructor function in JavaScript. Since ES6 has the `class` keyword, a lot of people seem to think that solved many problems with constructor functions. It didn’t. Let’s explore the major differences you still need to be aware of.

First, let’s look at examples of each:

```
// class
class ClassCar {
  drive () {
    console.log('Vroom!');
  }
}

const car1 = new ClassCar();
console.log(car1.drive());


// constructor
function ConstructorCar () {}

ConstructorCar.prototype.drive = function () {
  console.log('Vroom!');
};

const car2 = new ConstructorCar();
console.log(car2.drive());


// factory
const proto = {
  drive () {
    console.log('Vroom!');
  }
};

function factoryCar () {
  return Object.create(proto);
}

const car3 = factoryCar();
console.log(car3.drive());
```

Each of these strategies stores methods on a shared prototype, and optionally supports private data via constructor function closures. In other words, they have mostly the same features, and could mostly be used interchangeably.

In JavaScript, any function can return a new object. When it’s not a constructor function or class, it’s called a factory function.

In ES6 (ES2015) if you try to call a class constructor without `new`, it will always throw an error. It’s not possible to avoid forcing the `new` requirement on callers without wrapping your class in a factory function. There is a proposal for a future version of JavaScript to allow customizing the call behavior when callers omit `new`, but the proposal adds overhead to every class that uses it (meaning few will use it).

https://medium.com/siliconwat/how-javascript-classes-work-80b0cf483b1d
Class Methods are also just functions in JavaScript. Though it’s possible to define method functions inside the constructor, it’s inefficient as every new object created from the constructor will have redundant copies of the method definitions.

### It’s more efficient to define method functions on the prototype property of the constructor, which exists for this very reason.

https://stackoverflow.com/questions/49992687/do-we-still-need-prototype-in-es6-to-have-one-copy-of-a-method-shared-across-all

Your code excerpt translates to es2015 as follows:

```
function X() { }

X.prototype.f = function f() {
  return 'f';
};

let x1 = new X();

let x2 = new X();
x2.f = function() { return 'changed f'; };

console.log(x1.f()); // f
console.log(x2.f()); // changed f
```

https://hackernoon.com/understanding-javascript-new-keyword-ec67c8caaa74

## Factory pattern

https://medium.com/front-end-weekly/understand-the-factory-design-pattern-in-plain-javascript-20b348c832bd
One alternate way is to use objects

```
const Animal = {
name: "not_given_yet", //remove this if you like
walk() {
console.log(this.name + " walks");
}
}
const poo = Object.assign({}, Animal, {name: "poo"})
poo.walk()
or
const tommy = Object.create(Animal) //this sets up prototype chain
tommy.name = "tommy"
tommy.walk()
However I personally favor a different pattern called the Factory Design Pattern.

In a nutshell, if we implement instance creation inside the function itself and don’t require user to use Object.create or new keyword, then we have a factory.
```

## Object prototypes

https://www.w3schools.com/js/js_object_prototypes.asp
All JavaScript objects inherit properties and methods from a prototype.

In the previous chapter we learned how to use an object constructor:

```
function Person(first, last, age, eyecolor) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eyecolor;
}

var myFather = new Person("John", "Doe", 50, "blue");
var myMother = new Person("Sally", "Rally", 48, "green");
```

We also learned that you can not add a new property to an existing object constructor:
`Person.nationality = "English";`

To add a new property to a constructor, you must add it to the constructor function

All JavaScript objects inherit properties and methods from a prototype:

Date objects inherit from Date.prototype
Array objects inherit from Array.prototype
Person objects inherit from Person.prototype

Sometimes you want to add new properties (or methods) to all existing objects of a given type.

Sometimes you want to add new properties (or methods) to an object constructor.

The JavaScript prototype property allows you to add new properties to object constructors:

```
function Person(first, last, age, eyecolor) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eyecolor;
}

Person.prototype.nationality = "English";
```

https://hackernoon.com/prototypes-in-javascript-5bba2990e04b

When a function is created in JavaScript, the JavaScript engine adds a prototype property to the function. This prototype property is an object (called as prototype object) which has a constructor property by default. The constructor property points back to the function on which prototype object is a property. We can access the function’s prototype property using functionName.prototype.

As shown in the above image, Human constructor function has a prototype property which points to the prototype object. The prototype object has a constructor property which points back to the Human constructor function. Let’s see an example below:

## New Keyword

https://stackoverflow.com/questions/1646698/what-is-the-new-keyword-in-javascript
It creates a new object. The type of this object is simply object.
It sets this new object's internal, inaccessible, [[prototype]] (i.e. **proto**) property to be the constructor function's external, accessible, prototype object (every function object automatically has a prototype property).
It makes the this variable point to the newly created object.
It executes the constructor function, using the newly created object whenever this is mentioned.
It returns the newly created object, unless the constructor function returns a non-null object reference. In this case, that object reference is returned instead.

Once this is done, if an undefined property of the new object is requested, the script will check the object's [[prototype]] object for the property instead. This is how you can get something similar to traditional class inheritance in JavaScript.

The most difficult part about this is point number 2. Every object (including functions) has this internal property called [[prototype]]. It can only be set at object creation time, either with new, with Object.create, or based on the literal (functions default to Function.prototype, numbers to Number.prototype, etc.). It can only be read with Object.getPrototypeOf(someObject). There is no other way to set or read this value.

## Object Methods

https://www.w3schools.com/js/js_object_methods.asp

```

```
