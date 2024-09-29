Hello fellow Tech enthusiasts!!!. This is a repository that explains the common practices and advanced javascript concepts

#Data Types

JavaScript has a variety of data types that can be categorized into two broad categories - Primitive Types and Object Types.
Understanding these types is essential as they dictate how data is stored, manipulated, and passed around in JavaScript.

### Primitive Types
Primitive types are the most basic data types in JavaScript, and they are immutable. When you work with a primitive type, you are working directly with the actual value.

🎯 **Number**
Represents both integers and floating-point numbers.
JavaScript uses double-precision 64-bit binary format (IEEE 754 standard) for representing numbers.
Special values: Infinity, -Infinity, and NaN (Not a Number).
```js
let integer = 42;
let float = 3.14;
let infinityValue = Infinity;
let notANumber = NaN;
```
🎯 **String**

A sequence of characters enclosed in quotes (single ', double ", or backticks for template literals).
Strings are immutable; modifying a string creates a new string.
```js
let singleQuoteStr = 'Hello';
let doubleQuoteStr = "World";
let templateLiteral = `Hello, ${doubleQuoteStr}!`; // Template literals support interpolation
```
🎯 **Boolean**

Represents a logical value: true or false.
```js
let isTrue = true;
let isFalse = false;
```
🎯 **Undefined**

A variable that has been declared but has not been assigned a value.
```js
let uninitializedVar;
console.log(uninitializedVar); // undefined
```
🎯 **Null**

Represents the intentional absence of any object value. It is used to indicate that a variable should have no value.

```js
let emptyVar = null;
```
🎯 **Symbol (introduced in ES6)**

A unique and immutable data type often used for object property keys.
Each Symbol is unique, even if they have the same description.
```js
let symbol1 = Symbol('description');
let symbol2 = Symbol('description');
console.log(symbol1 === symbol2); // false
```
🎯 **BigInt (introduced in ES11/ES2020)**

Used to represent integers with arbitrary precision. This is useful for working with very large numbers that cannot be represented by the Number type.
```js
let bigIntNumber = 1234567890123456789012345678901234567890n;
console.log(bigIntNumber); // Outputs a BigInt value
```

### Object Types

Objects in JavaScript are more complex and can hold multiple values as properties. Unlike primitives, objects are mutable and store references to their values.

🎯 **Object**

A collection of key-value pairs, where keys (also called properties) are strings (or Symbols), and values can be of any data type.
Objects are created using the object literal {} or the new Object() syntax.
```js
let person = {
  name: "John",
  age: 30
};
console.log(person.name); // "John"
```
🎯 **Array**

A special type of object that holds an ordered list of values (elements).
Arrays are indexed starting from 0 and can hold any data type, including other arrays.
```js
let arr = [1, "Hello", true];
console.log(arr[1]); // "Hello"
```

🎯 **Function**

A function is a special kind of object. Functions in JavaScript can be assigned to variables, passed as arguments, and returned from other functions.
```js
function greet() {
  return "Hello!";
}
console.log(greet()); // "Hello!"
```
🎯 **Date**

Used to work with dates and times.
```js
let currentDate = new Date();
console.log(currentDate); // Current date and time
```

🎯 **RegExp (Regular Expression)**

Represents a pattern for matching strings.

```js
let regex = /hello/i;
console.log(regex.test("Hello world!")); // true
```

🎯 **Map and Set (introduced in ES6)**

Map: A collection of key-value pairs, where keys can be of any data type (not limited to strings).
Set: A collection of unique values, where duplicate values are not allowed.
```js
let map = new Map();
map.set("key", "value");
console.log(map.get("key")); // "value"

let set = new Set();
set.add(1);
set.add(1); // Duplicate, ignored
console.log(set.size); // 1
```
## Differences Between Primitive and Object Types

### _**Mutability:**_

- Primitive types are immutable (cannot be altered once created).
- Object types are mutable (their values can be changed after they are created).
```js
let str = "Hello";
str[0] = "h";  // Strings are immutable, so this does nothing.
console.log(str); // "Hello"

let obj = { name: "John" };
obj.name = "Doe";  // Objects are mutable, so this works.
console.log(obj.name); // "Doe"
```
### _**Storage:**_

Primitive types are stored directly by value.
Object types are stored by reference. When an object is assigned to a variable, that variable holds a reference (or pointer) to the object, not the actual object itself.
```js
let a = 10;
let b = a;  // Copy of value
b = 20;
console.log(a); // 10, because `a` holds the original value

let obj1 = { name: "John" };
let obj2 = obj1;  // Reference to the same object
obj2.name = "Doe";
console.log(obj1.name); // "Doe", because both `obj1` and `obj2` refer to the same object
```
### _**Comparison:**_

Primitive types are compared by value.
Object types are compared by reference.
```js
let num1 = 10;
let num2 = 10;
console.log(num1 === num2); // true, because they have the same value

let obj1 = { name: "John" };
let obj2 = { name: "John" };
console.log(obj1 === obj2); // false, because they are different objects in memory
```
### Summary

<img width="535" alt="image" src="https://github.com/user-attachments/assets/b4083906-8e3f-4285-90f7-f53f11c02e0f">


# JavaScript Scopes

In JavaScript, there are several kinds of scopes that determine the visibility and lifespan of variables. These include **Global Scope**, **Function Scope**, **Block Scope**, and **Module Scope**. Understanding these helps in writing more organized and efficient code.

## 1. Global Scope

- Variables declared in the global scope are accessible anywhere in the program.
- In browsers, the global scope is typically the `window` object.

### Example:

```javascript
var globalVar = "I am global";

function logGlobalVar() {
  console.log(globalVar); // Accessible
}

logGlobalVar();
console.log(globalVar); // Accessible globally
```
Here, globalVar is available inside and outside the function because it’s in the global scope.

## 2. Function Scope
Variables declared inside a function are only accessible within that function. They cannot be accessed outside of the function.
functionScopedVar is function-scoped.

Example:
```js
function functionScopeExample() {
  var functionScopedVar = "I exist only in this function";
  console.log(functionScopedVar); // Accessible within the function
}

functionScopeExample();
console.log(functionScopedVar); // Error: functionScopedVar is not defined
```
Here, functionScopedVar is not accessible outside the functionScopeExample function.

## 3. Block Scope
Variables declared with let or const are block-scoped, meaning they are only accessible within the block they are declared in (i.e., within {}).
This can include loops, if statements, or any other code block.

Example:
```js
if (true) {
  let blockScopedVar = "I am block scoped";
  console.log(blockScopedVar); // Accessible within this block
}

console.log(blockScopedVar); // Error: blockScopedVar is not defined
```
In this case, blockScopedVar is only available within the if block.

## 4. Module Scope (Introduced in ES6)
JavaScript modules have their own scope. Variables, functions, and classes declared in a module are not accessible outside the module unless explicitly exported.
Similarly, a module's contents are not accessible in the global scope unless imported.

Example (in a module):
```js
//module.js
export const moduleVar = "I am module scoped";
export function moduleFunction() {
  console.log("Module function");
}
```
```js
//main.js
import { moduleVar, moduleFunction } from './module.js';

console.log(moduleVar); // Accessible due to explicit import
moduleFunction(); // Accessible due to explicit import
```
In this example, the variables and functions declared in module.js are not available globally. They are only accessible if imported in another module.

## Summary of Scopes
- **Global Scope:** Variables available everywhere in the program.
- **Function Scope:** Variables defined within a function and only accessible within that function.
- **Block Scope:** Variables declared with let or const inside {} are only accessible within that block.
- **Module Scope:** Variables and functions inside a module are only accessible when exported and imported.

# Hoisting 

Hoisting in JavaScript is a behavior in which variable and function declarations are moved to the top of their containing scope (global or function) during the compilation phase. This means that you can use variables and functions before they are declared in your code, but only the declarations (not initializations) are hoisted.

### Key Points:
🎯 Only declarations are hoisted, not initializations.
- Variables declared with var are hoisted, but their initial values are not.
- Functions declared using function declarations are fully hoisted.
- Variables declared with let and const are also hoisted but are placed in the temporal dead zone until the actual line of declaration is 
  reached, meaning you can’t use them before they are declared.
  
Example of Variable Hoisting with var:
```js
console.log(hoistedVar);  // Outputs: undefined
var hoistedVar = "I am hoisted!";
console.log(hoistedVar);  // Outputs: I am hoisted!
```
Explanation:
The declaration var hoistedVar is hoisted to the top, but its initialization (hoistedVar = "I am hoisted!") is not. Before the line var hoistedVar is executed, hoistedVar is undefined.

Example of Function Hoisting:
```js
hoistedFunction();  // Outputs: I am hoisted!

function hoistedFunction() {
  console.log("I am hoisted!");
}
```
Explanation:
Function declarations are fully hoisted, meaning the entire function (not just its name) is moved to the top of the scope. As a result, you can call hoistedFunction() before its declaration.

### Hoisting with let and const:
```js
console.log(letVar);  // ReferenceError: Cannot access 'letVar' before initialization
let letVar = "I am not hoisted like var!";
```
Explanation:
Although let and const declarations are hoisted, they are not initialized until their actual declaration is encountered in the code. This results in a ReferenceError if you try to access them before the line where they are declared.

### Summary of Hoisting Behavior:
- _var:_   Hoisted with an initial value of undefined. You can reference the variable before it's declared, but it will be undefined until it is assigned a value.
- _let and const:_   Hoisted but not initialized. Accessing them before their declaration causes a ReferenceError.
- _Functions (using function declarations):_    Fully hoisted, allowing you to call the function before its declaration.

Example to Illustrate Hoisting:
```js
// Variable hoisting with `var`
console.log(varVar); // undefined
var varVar = "Hoisted var";
console.log(varVar); // "Hoisted var"

// Variable hoisting with `let`
try {
  console.log(letVar); // ReferenceError
} catch (e) {
  console.log(e.message);
}
let letVar = "Not hoisted like var";

// Function hoisting
hoistedFunction(); // "Hoisted function"

function hoistedFunction() {
  console.log("Hoisted function");
}
```
## Why Does Hoisting Happen?
JavaScript's interpreter splits the code into two phases:**
- _Compilation phase:_**  The interpreter scans the code and hoists all declarations to the top of the scope (global or function).
- **_Execution phase: _**  The code is executed line by line in the order it is written, but since declarations are hoisted, they are already processed by this point.
  
This behavior of hoisting is one of the quirks of JavaScript that developers must be aware of to avoid potential pitfalls.

# When should you choose to use “let” or “const”

_**let**_ and **_const_** were introduced in JavaScript with the release of ECMAScript 6 (ES6) in 2015. They provide block-scoped variables and constants, which offer more predictable and manageable scoping behavior compared to the traditional var.

Before ES6, var was the only way to declare variables. It has several shortcomings:

❌ _Function Scope:_ Variables declared with **var** are function-scoped, which can lead to confusion and errors, especially in larger codebases.

```js
function example() {
  if (true) {
    var x = 5;
  }
  console.log(x); // 5 (x is function-scoped, not block-scoped)
}
example();
```

❌ _Hoisting:_ Variables declared with **var** are hoisted to the top of their enclosing function or global scope, which can lead to unexpected behavior.

```js
console.log(x); // undefined (x is hoisted but not initialized)
var x = 10;
```

❌ _No Block Scope:_ **var** does not respect block scope, which can cause variables to be accessible outside of the intended block.

```js
if (true) {
  var x = 10;
}
console.log(x); // 10 (x is accessible outside the block)
```

_**"let"**_

- _Block Scope:_ Variables declared with **let** are limited to the block, statement, or expression in which they are used.
- _No Hoisting:_ While **let** variables are hoisted to the top of their block, they are not initialized until the let statement is executed. This results in a "temporal dead zone" from
  the start of the block until the declaration is encountered.
- _Reassignment:_ Variables declared with **let** can be reassigned.

```js
let x = 10;
if (x > 5) {
  let y = x + 5;
  console.log(y); // 15
}
console.log(y); // ReferenceError: y is not defined
```

**_"const"_**

- _Block Scope:_ Like **let**, variables declared with const are block-scoped.
- _No Hoisting:_ The **const** variables are not hoisted to the top of their block, but not initialized until **const** statement is executed similar to **let**. This also results in "temporal dead
  zone"
- _No Reassignment:_ Variables declared with **const** cannot be reassigned. They are read-only after the initial assignment.
- _Immutable Binding:_ While the binding is immutable, the content of the variable (such as an object or array) can still be modified.

```js
const x = 10;
x = 20; // TypeError: Assignment to constant variable.

const arr = [1, 2, 3];
arr.push(4); // This is allowed
console.log(arr); // [1, 2, 3, 4]
```

```js
console.log(x); // ReferenceError: Cannot access 'x' before initialization
let x = 10;
console.log(x); // 10

console.log(y); // ReferenceError: Cannot access 'y' before initialization
const y = 20;
console.log(y); // 20

console.log(z); // undefined
var z = 30;
console.log(z); // 30
```

### When to Use let and const

- _const:_ we should use **const** for declaring variables that should not be reassigned and which should be treated as constants. Using const by default is generally suggested as it makes our code easier to understand and more predictable.

```js
const PI = 3.14;
```

- _let:_ We should use **let** while declaring variables that need to be reassigned Use let when you need to reassign a variable. This is typically used for loop counters, variables that will change value, or in situations where the variable needs to be initialized later.

```js
let counter = 0;
counter++;
```

## An example of a common mistake related to hoisting and how to fix it

Most often, common mistakes related to hoisting will happen while trying to access variable declared with **var** before it's declaration. When a variable is declared with var, only the declaration is hoisted to the top of the scope, not the variable initialization.

```js
console.log(x); // Outputs: undefined
var x = 5;
console.log(x); // Outputs: 5
```

We can fix this in two simple ways:

- Always following the conventional practice of declaring and initializing variable at the top of the scope before trying to access the variable.

```js
var x = 5;
console.log(x); // Outputs: 5
console.log(x); // Outputs: 5
```

- Use **let** or **const** to declare a variable. Using let or const creates a "temporal dead zone" from the start of the block until the declaration is processed. This means that if you try to access the variable before it's declared, you'll get a ReferenceError, which is often more helpful for debugging than the undefined behavior of var.

```js
console.log(x); // Throws ReferenceError: Cannot access 'x' before initialization
const x = 5;
console.log(x); // This line is never reached due to the error
```

Another common mistake is using **var** in loops, which can lead to unexpected behavior due to its function-scoped nature.

```js
for (var i = 0; i < 3; i++) {
  setTimeout(function () {
    console.log(i); // 3, 3, 3
  }, 1000);
}
```

The var i declaration is hoisted to the function scope.
By the time the setTimeout callback runs, the loop has completed, and i is 3.

We can fix this mistake by declaring loop variables with **let**. Using **let** in the loop will create a new binding for each iteration, preserving the expected behavior.

```js
for (let i = 0; i < 3; i++) {
  setTimeout(function () {
    console.log(i); // 0, 1, 2
  }, 1000);
}
```

The **let** i declaration is block-scoped.
Each iteration of the loop creates a new i, preserving the value for the _setTimeout_ callback.


# What are closures in JavaScript?

### [Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures#creating_closures_in_loops_a_common_mistake) :

Closures in JavaScript are a powerful concept where an inner function retains access to variables from its outer function’s scope, even after the outer function has finished executing. This means that a function "remembers" the environment in which it was created.

Closure is a feature available in Java Script which enables a function to access a variable outside it's lexical scope even after the entity or function enclosing the function that is trying to access the variable has finished execution and has returned. In simple words, a closure gives you access to outer function's scope from inner function.


### How Closures Work:
When a function is declared inside another function, the inner function can access the variables defined in the outer function, even after the outer function has returned. This happens because of JavaScript’s function scope and its behavior of keeping references to variables in its environment, creating what is called a closure.

### Key Aspects of Closures:
* Lexical Scoping: The inner function has access to variables in three levels of scope:
* Variables in its own scope
* Variables in the outer function’s scope
* Global variables
* Persistent Data: Since the inner function keeps access to the outer function’s scope, the outer function’s variables are not discarded 
  when the outer function finishes. This allows the inner function to "close over" these variables, hence the term "closure."

Closure Example:
```js
function outerFunction(outerVariable) {
  return function innerFunction(innerVariable) {
    console.log('Outer Variable:', outerVariable);
    console.log('Inner Variable:', innerVariable);
  };
}

const closureExample = outerFunction('outside');
closureExample('inside'); 
```

In this example:

outerFunction creates a closure by returning innerFunction.
Even after outerFunction finishes, innerFunction can still access outerVariable because of the closure.

## Use Cases:
🎯 **_Data Privacy/Encapsulation:_**  Closures are often used to create private variables that can’t be accessed directly from the outside.
```js
//function to explain Data Privacy through closures
function createCounter() {
  let count = 0; // This is a private variable

  return {
    increment: () => {
      count++;
      return count;
    },
    decrement: () => {
      count--;
      return count;
    },
    getCount: () => {
      return count;
    },
  };
}

const counter = createCounter();

console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.decrement()); // 1
console.log(counter.getCount()); // 1
```
🎯 **_Function Factories:_** Closures allow you to create function factories, which return functions customized by their environment.
```js
function createMultiplier(multiplier) {
  return function(value) {
    return value * multiplier;
  };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5)); // 10
console.log(triple(5)); // 1
```
🎯 **_Callbacks and Event Listeners:_** Closures are commonly used in asynchronous code such as callbacks, event listeners, and promises.
```js
function fetchData(url) {
  let data = 'Data from ' + url;
  return function() {
    console.log(data);
  };
}

const displayData = fetchData('https://example.com');
displayData(); // Logs 'Data from https://example.com'
```
🎯 **_Maintainining State:_** closures are also useful in maintaining state between function calls without using global variables. This is particularly useful in scenarios when we need to cache cost expensive function calls.

```js
//Function to explain memorization and state maintenance using closures
function memoize(fn) {
  const cache = {};

  return function (...args) {
    const key = JSON.stringify(args);
    if (cache[key]) {
      return cache[key];
    }
    const result = fn(...args);
    cache[key] = result;
    return result;
  };
}

function fibonacci(n) {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}

const memoizedFibonacci = memoize(fibonacci);

console.log(memoizedFibonacci(10)); // 55
console.log(memoizedFibonacci(10)); // 55 (retrieved from cache)
console.log(memoizedFibonacci(20)); // 6765
console.log(memoizedFibonacci(20)); // 6765 (retrieved from cache)
```

