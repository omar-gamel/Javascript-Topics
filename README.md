# What is js hosting ?

<b>Hoisting is a behavior in JavaScript where variable and function declarations are moved to the top of their containing scope before code execution.</b> Regardless of where functions and variables are declared, they are moved to the top of their scope by the JavaScript interpreter. This means that you can use variables and functions before you declare them in your code. However, the hoisting behavior works differently for variables declared with <b>var</b>, <b>let</b>, or <b>const</b> and for function declarations and expressions.

<h3>Variables Hoisting:</h3>

1. <b>var:</b> When you declare a variable using var, the variable declaration is hoisted to the top of its current scope, but the assignment of its value is not hoisted.
``` javascript
console.log(myVar); // undefined, not ReferenceError
var myVar = "Hello";
```
In this example, the declaration of myVar is hoisted to the top, but its assignment (<b>"Hello"</b>) is not. That's why it logs <b>undefined</b> instead of throwing a <b>ReferenceError.</b>

2. <b>let</b> and <b>const:</b> Unlike var, when you declare variables with <b>let</b> or <b>const</b>, they are not initialized during hoisting. If you try to access them before the declaration, you get a ReferenceError.
 ``` javascript
console.log(myLet); // ReferenceError: Cannot access 'myLet' before initialization
let myLet = "Hello";
```

<h3>Function Hoisting:</h3>

1. <b>Function Declarations:</b> In JavaScript, function declarations are hoisted to the top of their enclosing scope.
declaration, you get a ReferenceError.
 ``` javascript
hello(); // Outputs: "Hello world!"

function hello() {
  console.log("Hello world!");
}
```
The function <b>hello()</b> can be called before its declaration because the function definition is hoisted to the top of the scope.

 2. <b>Function Expressions:</b> If you define a function using a function expression, the variable name is hoisted, but the function's body and assignment are not.
``` javascript
hello(); // TypeError: hello is not a function

var hello = function() {
  console.log("Hello world!");
};
```
In this case, <b>hello</b> is hoisted as a variable (with <b>var</b>), but since its assignment to a function happens at runtime, trying to invoke <b>hello</b> before the assignment results in a <b>TypeError.</b>

# What is js Closures ?

<b>closures are functions that have access to the parent scope</b>, even after the parent function has closed. This is a powerful feature of JavaScript that allows for encapsulation and the creation of private variables. Here's a deeper dive into closures with an example:

<h3>Understanding Closures:</h3>

When you define a function within another function, the inner function has access to the variables of the outer function even after the outer function has finished executing. This behavior is what defines a closure.

``` javascript
function createGreeting(greetingPrefix) {
  return function(name) {
    console.log(greetingPrefix + ' ' + name);
  };
}

const sayHello = createGreeting('Hello');
const sayHi = createGreeting('Hi');

sayHello('John'); // Outputs: "Hello John"
sayHi('Jane'); // Outputs: "Hi Jane"
```

# Pure function vs Impure functions

<h3>Pure Function</h3> 

<b>pure function is a function that always returns the same output for the same input and does not cause any side effects.</b> In other words, it only depends on its input parameters and does not modify any external state or global variables. Pure functions are deterministic, meaning that they will always produce the same output given the same input, which makes them easy to test, maintain, and reason about.

Here's an example of a pure function:

``` javascript
function add(a, b) {
 return a + b;
}
```

This function takes two input parameters and always returns the same output for the same input, without modifying any external state or variables. It does not cause any side effects.

<h3>Impure Function</h3> 

<b>impure function is a function that can cause side effects and modify external state or global variables.</b> This makes it harder to predict and reason about, and it can lead to bugs and unexpected behavior. Examples of impure functions include functions that modify the DOM, interact with external APIs or databases, and generate random numbers.

Here's an example of an impure function:

``` javascript
let counter = 0

function increment() {
 counter++;
 console.log(counter);
};
```

This function modifies the external counter variable and logs the updated value to the console. This makes it impure because it causes a side effect and modifies the external state.

# Arrow Functions vs Regular Functions

<h3>1. Regular Function Syntax vs Arrow Function Syntax</h3>

<b>Regular function syntax:</b>

``` javascript
function sayHello(name) {
  return 'Hello ' + name
}
```

<b>Arrow function syntax:</b>

``` javascript
const sayHello = (name) => {
  return 'Hello ' + name
}
```

<h3>2. How to Access the Arguments Passed to Functions</h3>

<b>How to access arguments with regular functions:</b>

You can access all the arguments passed to a regular function using the <b>arguments</b> object. The <b>arguments</b> object is an array-like object that holds all the arguments passed to the function.

``` javascript
function logNumbers(num1, num2) {
  console.log(arguments)
}

logNumbers(8, 24)  // Output: Arguments(2) i { 0:8, 1:24 }
```

<b>How to access arguments with arrow functions:</b>

The <b>arguments</b> object is not available in arrow functions. If you try to access it in arrow functions, JavaScript will throw a reference error.

``` javascript
const logNumbers = (num1, num2) => {
  console.log(arguments)
}

logNumbers(8, 24) // Uncaught ReferenceError: arguments is not defined
```

To access the arguments passed to an arrow function, you can use the rest parameter syntax (__...__).

``` javascript
const logNumbers = (...args) => {
  console.log(args)
}

logNumbers(8, 24) // Output: (2) [8, 24]
```

<h3>3. Duplicate Named Parameters</h3>

<b>Duplicate named parameters in regular functions:</b>

When a regular function has duplicate names in the parameters, the last parameter with the duplicate name will take precedence.
``` javascript
function exampleFunction(a, b, a) {
  console.log(a, b)
}

exampleFunction("first", "second", "third") // third second
```

But in "strict mode", using a duplicate named parameter will result in a syntax error.
``` javascript
"use strict"

function exampleFunction(a, b, a) {
  console.log(a, b)
}

exampleFunction("first", "second", "third") // SyntaxError: Duplicate parameter not allowed in this context
```

<b>Duplicate named parameters in arrow functions:</b>

Arrow functions don't allow for the same parameter name to be used more than once in the parameter list. Doing so will result in a syntax error.
``` javascript
const exampleFunction = (a, b, a) => {
  console.log(a, b)
}

exampleFunction("first", "second", "third") // SyntaxError: Duplicate parameter not allowed in this context
```

<h3>4. Function Hoisting</h3>

<b>Hosting in regular functions:</b>

Regular functions are hoisted to the top. And you can access and call them even before they are declared.
``` javascript
regularFunction() 

function regularFunction() {
  console.log("This is a regular function.")
}
```
<b>Hosting in regular functions:</b>

Arrow functions, on the other hand, cannot be accessed before they are initialised.
``` javascript
arrowFunction() // Uncaught ReferenceError: Cannot access 'arrowFunction' before initialization

const arrowFunction = () => {
  console.log("This is an arrow function.")
}
```

<h3>5. How to Handle this Binding in Functions</h3>

- <b>Regular functions:</b> have their own <b>this</b> context. And this is determined dynamically depending on how you call or execute the function.

- <b>Arrow functions:</b> on the other hand, do not have their own this context. Instead, they capture the <b>this</b> value from the surrounding lexical context in which the arrow function was created.

<b>1. Setting the this value during a simple function call</b>
- <b>regular functions:</b> a simple function call sets the <b>this</b> value to the <b>window</b> object (or to <b>undefined</b> if you're using the "strict mode"):

``` javascript
function myRegularFunction() {
  console.log(this)
}
    
myRegularFunction() // Window
```

``` javascript
"use strict"

function myFunction() {
  console.log(this)
}
    
myFunction() // udefined
```
- <b>arrow functions:</b> a simple function call sets the <b>this</b> value to the surrounding context whether you're using strict mode or not. In the example below, the surrounding context is the global window object.
``` javascript
const myArrowFunction = () => {
  console.log(this);
};

myArrowFunction() // Window
```

<b>2. When invoking or calling a method on an object</b>

When you invoke a method whose value is a regular function, the <b>this</b> value is set to the object on which the method is called. But when the value of the method is an arrow function, the <b>this</b> value is set to the global window object.
``` javascript
const myObject = {
  regularExample: function() {
    console.log("REGULAR: ", this)
  },
    
  arrowExample: () => {
    console.log("ARROW: ", this)
  }
}
    
myObject.regularExample() // {regularExample: f, arrowExample: f}
myObject.arrowExample() // Window
```
<h3>6. How to Use Functions as Constructors</h3>

- <b>regular functions:</b> you can create a <b>new</b> instance using the new keyword. And this sets the <b>this</b> value to the new instance you've created.

- <b>arrow functions:</b> you cannot use them as constructors. This is because the value of <b>this</b> in arrow functions is lexically scoped – that is, determined by the surrounding execution context. This behaviour does not make them suitable to be used as constructors.

Here's an example:

``` javascript
function RegularFuncBird(name, color) {
  this.name = name
  this.species = color
  console.log(this)
}

const ArrowFuncBird = (name, color) => {
  this.name = name
  this.color = color
  console.log(this)
}

new RegularFuncBird("Parrot", "blue")  // {name: 'Parrot', species: 'blue'}
new ArrowFuncBird("Parrot", "blue") // TypeError: ArrowFuncBird is not constructor
```

<h3>7. So Which One Should You Use?</h3>

There is no straightforward answer to this. Whether you use a regular function or arrow function depends on the specific use case.

It's recommended to use regular function in any of the following cases:

- when you need to use a constructor with the <b>new</b> keyword
- when you need the <b>this</b> binding to be dynamically scoped
- when you want to use the arguments object
  
And you can use <b>arrow</b> functions in any of the following cases:

- when you want a more concise syntax for the function
- when you need to maintain the lexical scope of <b>this</b>
- for non-method functions (in most cases)

# Callbacks vs. Promises vs. Async/Await: Detailed Comparison

<b>Callback</b>, <b>Promise</b>, and <b>async/await</b> are all mechanisms used in JavaScript for handling asynchronous operations. Let's compare them based on various aspects:

1. <b>Readability:</b>
   - <b>Callbacks:</b> Callbacks can lead to "callback hell" where multiple nested callbacks make code hard to read and maintain.
   - <b>Promise:</b> Promises provide a cleaner alternative to callbacks with chaining <b>.then()</b> calls, improving readability to some extent.
   - <b>Async/await:</b> Async/await offers the most readable syntax by allowing asynchronous code to be written in a synchronous manner, making it easier to understand.

2. <b>Error Handling:</b>
   - <b>Callbacks:</b> Error handling in callbacks can be cumbersome and prone to errors, especially with nested callbacks.
   - <b>Promise:</b> Promises have built-in error handling with the <b>.catch()</b> method, allowing for more structured error handling.
   - <b>Async/await:</b> Error handling with async/await is similar to synchronous code using try/catch blocks, making it intuitive and easy to handle errors.
  
3. <b>Chaining:</b>
   - <b>Callbacks:</b> Chaining callbacks can lead to deeply nested code, which is difficult to manage.
   - <b>Promise:</b> Promises support chaining <b>.then()</b> calls, allowing for sequential execution of asynchronous operations in a more readable way.
   - <b>Async/await:</b> Async/await allows sequential code execution without nesting, making it easier to reason about and maintain.
  
4. <b>Error Propagation:</b>
   - <b>Callbacks:</b> Error propagation in callbacks can be challenging, often requiring manual handling and passing errors through each callback.
   - <b>Promise:</b> Promises propagate errors automatically down the chain, simplifying error handling.
   - <b>Async/await:</b> Errors in async/await functions propagate automatically, making error handling straightforward.

# What is JavaScript scope?

 <b>In JavaScript, scope refers to the current context of your code. This context determines where you can access certain variables and functions. In other words, where you decide to define a variable or function in JavaScript impacts where you have access to it later on.</b> So, if you define a variable inside a function, you will only be able to access it inside that function.

<p align="center">
  <img src="https://github.com/omar-gamel/javascript-topics/blob/main/scope.PNG" alt="Type of Js Scopes" width="500" height="400">
</p>

 <h3>Global Scope</h3>
Global scope means that a variable or function is available anywhere in your code. This is the default scope for variables and functions in JavaScript.Let's take a look at an example:
 
 ``` javascript
  var pet = 'dog';
  function printPet() {
      console.log(pet); // prints 'dog' to the console
  }
 ```

 <h3>Function Scope</h3>
 Function scope is similar to a local scope in that variables and functions defined inside a function are only available inside that function. However, there is one key difference: variables and functions defined inside a function are not available in the global scope.Let's take a look at an example:

``` javascript
function printPet() {
    var pet = 'cat';
    console.log(pet); // prints 'cat' to the console
} 
```

 <h3>Block Scope</h3>
 Block scope allows us to create variables and functions only available inside a code block. A code block is any time you use curly braces, for example:

``` javascript
if (true) {
    // this is a code block 
} else {
    // this is also a code block
} 
```

 <h3>Lexical Scope</h3>
 Lexical scope can be a bit more complicated than the other types of scope. It is sometimes also called static scope or compile-time scope.Lexical scope means that the scope of a variable is determined by its position in the code. In other words, variables are available in the same scope as their parent variables.For example:

``` javascript
var pet = 'cat';
function printPet() {
    console.log(pet); // prints 'cat' to the console
}
```
