Hello fellow Tech enthusiasts!!!. This is a repository that explains the common practices and advanced javascript concepts

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

