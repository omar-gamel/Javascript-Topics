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
