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
   
