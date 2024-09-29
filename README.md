Hello fellow Tech enthusiasts!!!. This is a repository that explains the common practices and advanced javascript concepts

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

### Why are closures useful in JavaScript?

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

