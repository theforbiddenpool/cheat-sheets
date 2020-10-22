`'use strict'` → enables Strict Mode, which catches common coding mistakes and "unsafe" actions.

__Falsy values__ → value that is considered false when encountered in a boolean context. In JavaScript, these are: `false`, `0`, `-0`, `""` [empty string], `NaN`, `undefined`, and `null`.

# The Inner-Workings of JavaScript
## Variable Scope
The scope of a variable is controlled by the location of the variable declaration. JavaScript currently has three scopes: 
- __global__ → variables declared outside of a function.
- __local__ → created by functions.
- __block__ → created by block structures, such as *for* and *if* statements. They are only created using the `let` and `const` keywords.

__Lexical (static) scope__ → the static structure of a program determines the variable scope. The JavaScript interpreter starts at the current executing scope, and works its way out until it finds the variable in question. If the variable is not found, then an exception is thrown.

## Hoisting
There are two fundamental concepts to understand hoisting: **declaration** and **assignment**.
```javascript
let state; // variable declaration
state = "ready"; // varible assignment

let state2 = "not ready"; // variable declaration + assignment
```
In this example, the last line of code, even though it seems like on state, the JavaScript engine treats it as two separate statements, like in the two first lines.

No matter where variables are declared within a particular scope, all variable declarations are move to the top of their scope (global or local). This is called **hoisting**. Any assignments are left in place.
```javascript
console.log(state) // output: undefined
var state = "ready";
```

With the new ES6 `let` or `const` keywords, this will result in a `ReferenceError`.
```javascript
console.log(state)
// ReferenceError: can't access lexical declaration 'state' before initialization

let state = "ready"
```

Hosting also affects function declarations.
```javascript
showState() // output: Ready

function showState() {
  console.log('Ready')
}
```

Functions are hoisted first, then variables.

# Functions
> A function is a mapping between an input and an output.

There are several rules a function must follow to be considered a function:
- Multiple inputs can map to a single input.
- Same input cannot map to multiple inputs.

In JavaScript, a function always returns something. If we don't specify what that something is, JS will return `undefined` for us. If the function doesn't return anything, we might be getting our return some place else. In that case, it's an **impure function** and its causing a side-effect. We should avoid doing that whenever possible.

### Function declaration vs. Function assignment
```javascript
function showState() {} // function declaration
const showState2() = function() {} //function expresson
```

### Functions As First-Class Objects
__First-class citizenship__ → an entity supports all the operational properties inherent to other entities. In other words, means "being able to do what everyone else can do".

Why are functions first-class objects in JavaScript?
- functions are objects. They inherit from the Object prototype.
- can be assigned to key-value pairs.
- can be assigned to variables.
- can be passed as arguments.
- can be assigned as the return value of other functions.

This allows a lot of flexibility, and it's one of the bases of **functional programming**. Being able to pass a callback to event listeners is a very useful feature. It also allows the creation of closures and partial-application/currying.

## Recursive Functions
A function that calls itself to do something or get a result is a **recursive function**. The most basic example of one is the implementation of factorial:
```javascript
function fac(n) {
  if (n === 0) return 1 // this is our rule number 1 being satisfied.
  return n * fac(n-1) // rule number 2 being satisfied
}
```

In every recursion, there are always at least 2 logical cases:
1. a base where the function does not call itself, so the recursion doesn't keep running indefinitely.
2. the recursive call.

> __Note:__ In JavaScript, recursion is usually fine for simple algorithms that don't need too many recursive calls. If that happens, the algorithm is either not going perform well or going to crash because of stack overflow.

Most loops can be rewritten in a recursive style, however most JavaScript compilers are not currently optimized to support them safely.

Recursion is best applied when we need to call the same function repeatedly with different parameters from within a loop, *e.g.* fractal math, sorting, or traversing the nodes of complex or non-linear data structures. It allows for the construction of stateless code.

### Tail Call Optimization
Most implementations of JavaScript don't have a standard way to prevent recursive functions from stacking up on themselves indefinitely.

In many functional languages, such as Haskell, this is managed using a technique called **tail call optimization**. With tail call optimization each successive cycle in a recursive function takes place immediately, instead of stacking up in memory.

Theoretically, this is part of the standard for ECMAScript 6, however it has yet to be fully implemented by most platforms.

### Trampoline Functions
It's possible to construct a custom **trampoline function** to manage recursive execution iteratively, keeping only one operation on the stack at a time.

However, this usually slows down performance in favor of safety. Additionally, much of the readability of recursive functions is lost.

## Higher-Order Functions
A **Higher-Order Function** is a function that maps:
- from function to output;
- from input to function;
- from function to function.

An example from input to function is:
```javascript
function add(a) {
  return function (b) {
    return a + b;
  }
}

let addOne = add(1) // returns a function
let addTen = add(10) // also returns a function

addTen(1) // returns 11
```

## Closures
__Closure__ → inner function that has access to the parent function's scrope, even after the parent function has finished executing.
```javascript
function makeCounter() {
  let counter = 0;

  function make() {
    counter += 1;
    return counter;
  }

  return make;
}

const myCounter = makeCounter()

console.log(myCounter()); // Output: 1
console.log(myCounter()); // Output: 2
```
Closures internally store references to their *outer varibles*, and can access and update their values. When the outer function has finished executing, no other part of the code can access or manipulate the `counter` variable.

## Currying
It's when a function takes its arguments one at a time.
```javascript
const add = function(x) {
  return function(y) {
    return x + y
  }
}

const add10 = add(10)
add(10) // 20
add(20) // 30
```

## ES6
Arrow function → `(x, y) => {}`\
Implicit return with arrow functions → `() => 'value'`

Default parameter → `function greeting(name = 'Anonymous') {}`

### Arrow Function vs. Regular Function
1. __`arguments` binding__ → arrow functions don't have `arguments` binding. However, it has access to the closest `arguments` object of non-arrow parent function.
2. __`this` keyword__ → the value of `this` is always bound to the value of `this` in the closest non-arrow parent function.
3. __`new` keyword__ → arrow functions are only callable and not constructible. They can never be invoked with the `new` keyword.
4. __No duplicate named parameters__ → when not using `strict` mode in JavaScript, parameters can have the same name (*e.g.* `function add(x, x){}`). In arrow functions, this is never allowed.

### Rest operator
The rest operator (`...`) can be used where multiple parameters are expected.
```javascript
function func1(arg1, arg2, ...args) {
  ...
}
```
The `args` variable will be an array containing all the remaining passed arguments.

## `apply`, `call`, and `bind` Methods
This methods are deeply related to the `this` keyword. They are available to all functions due being inherited through the `Function.prototype` chain.

- `Function.prototype.apply` → calls a function with a given `this` value, and arguments provided as an array-like object. `apply` will take all the values inside the array as individual arguments and then apply the function to them. A common use is finding the maximum value within an array.
```javascript
const numbers = [53, 65, 25, 37, 78]

console.log(Math.max(numbers))
// output: NaN

console.log(Math.max.apply(null, numbers))
// output: 78
```
- `Function.prototype.call` → calls a function with a given `this` value and arguments provided individually. It's similar to `apply`, the only difference being that, instead of an array, the arguments are provided individual to the `call` function. Often used with constructor chaining.
```javascript
function sleep() {
  const reply = [this.animal, 'typically sleep between', this.sleepDuration].join(' ')
  console.log(reply)
}

const obj = {
  animal: 'Dogs', sleepDuration: '12 and 14 hours'
}

sleep.call(obj)
```
- `Function.prototype.bind` → creates a new function that, when called, has its `this` keyword set to the provided value, plus the provided arguments. The function returned is a special function object called **Bound function (BF)**. The BF wraps around the original function object.
```javascript
const x = 9
const module = {
  x: 81,
  getX: function() { return this.x }

  console.log(module.getX())
  // output: 81
  const retriveX = module.getX
  console.log(retrieveX())
  // output: 9
  const boundGetX = retrieveX.bind(module)
  console.log(boundGetX())
  // output: 81
}
```

# Destructuring Assignment
It's a special syntax for neatly assigning values taken directly from an object to variables.
```javascript
const { x, y, z } = voxel;
// OR
const { x: a, y: b, z: c } = voxel; // can be read as copy value form x to a
```

It can also be used in arrays:
```javascript
const [a, b] = [1, 2, 3];
const [c, d,,, e] = [1, 2, 3, 4, 5, 6];
const [a, b, ...arr] = [1, 2, 3, 4, 5];
```

We can use the destructuring assignment to pass an object as function parameters:
```javascript
const obj = { a = 1, b = 2, c = 3};

function ({ a, b }) {
  return a + b;
}
```

# Array Methods
Method | Description
--- | ---
`.push()` | adds a value to the end of array
`.unshift()` | adds a value to the beginning of array
`.pop()` | removes the last value and returns it
`.shift()` | removes the first value and returns it
`.splice(start, toRemove[, end])` | remove any number of consecutive elements from anywhere in an array
`.slice(start, end)` | copies a given number of elements to a new array
| | |
`.filter(func)` | filters the array accordingly with a condition
`.every(func)` | tests whether all elements in the array pass the test
`.some(func)` | tests whether at least one element in the array passes the test
`.map()` | creates a new array with the results of calling a provided function on every element in the calling array.
`.reduce()` | executes a reducer function (that you provide) on each element of the array, resulting in a single output value.
`.forEach()` | executes a provided function once for each array element
| | |
`.indexOf()` | return the index of specified element. If the element doesn't exist, returns `-1`.

### Method Chaining
```javascript
const squaredIntegers = arr
  .filter((value) => value > 0 && Number.isInteger(value))
  .map(value => value *= value);
```

## Spread Syntax
Allows an iterable such as an array or string to be expanded in function calls or array literals.
```javascript
const numbers = [1, 2, 3];
const numbers2 = [4, 5, 6];

console.log(sum(...numbers));

const numbers3 = [...numbers, ...numbers2];
```

# Objects
`delete myDog.tails` → deletes the property of the object.

`obj.hasOwnProperty()` → checks if the property of a given object exists or not.

`Object.freeze(obj)` → freezes an object so is no longer possible to add, update or delete properties from it.

`Object.keys(obj)` → generate an array which contains all the keys stored in an object.

`obj.constructor` → the property is a reference to the constructor function that created the instance. It's better to use `instanceof`.

### Tips
If you have tabular data, you can use an object to "lookup" values rather than a switch statement or an if/else chain.

## Optional Chaining (`?.`)
It allows reading the value of a property located within a chain of connected objects without having to expressly validade that each reference in the chain is valid.
```javascript
const person = {
  name: 'John',
  cat: {
    name: 'Murphy'
  }
}

const dogName = person.dog?.name
console.log(dogName)
console.log(person.nonExistentMethod?.())
// expected output: undefined
```

The expression returns `undefined` if the given property doesn't exist. Optional chaining cannot be used on a non-existent root object nor when is on the left side of the assignment.

A function's argument may have non-existent values. We can also use this operator to invoke a function if the function exist.
```javascript
function doSometing(onContent, onError) {
  try {
    // do something with the data
  } catch(err) {
    onError?.(err.message) // no exception if onError is undefined
  }
}
```

## Nullish Coalescing Operator (`??`)
It's a logical operator that returns its right-hand side operand when its left-hand side is `null` or `undefined`. Contrary to the logical OR (`||`), the left operand is only returned on this two values, avoiding unexpected behavior when using falsy values.
```javascript
const foo = null ?? 'default string'
console.log(foo)
// expected output: "default string"

const baz = 0 ?? 42
console.log(baz)
// expected output: 0
```

Parenthesis are needed to indicate precedence when using the nullish coalescing operator in combination with the AND (`&&`) and OR (`||`) operators. Otherwise, it will throw a `SyntaxError`.
```javascript
(null || undefined) ?? "foo"
```

# Math methods
`Math.random()` → generates random number from 0 to 1 (exclusive).

`Math.floor()` → rounds the number down to its nearest whole number.

`parseInt(str[, radix])` → converts string to number.
- `radix` → specifies the base for the number converted (from 2 [binary] to 36).

# Asynchronous Code
## SetTimeout & SetInterval
### Zero delay setTimeout `setTimeout(func)`
Schedules the execution of `func` **as soon as possible**. The scheduler will invoke it <mark>only after the current executing script is complete</mark>.

In the browser there is a limitation of how often nested timers can run: “after 5 nested timers, the interval is forced to be at least 4 milliseconds” ([HTML 5 standard](https://html.spec.whatwg.org/multipage/timers-and-user-prompts.html#timers)). It comes from ancient times and many scripts rely on it, so it exists for historical reasons. For server-side Javascript, that limitation does not exist.

### `setTimeout` With For Loop
> __Note:__ does not happen when using ES6 `let` keyword.
```javascript
var array = [1, 2, 3, 4, 5]

for(var i = 0; i < array.length; i++) {
  setTimeout(() => {
    console.log(array[i])
  }, 1000);
}

// i = 5
// console.log:
// undefined
// undefined
// undefined
// undefined
// undefined
```
The for loop exits before the setTimeout is triggered. Due to the closure created `i = 5`, therefore `array[5]` prints `undefined`. There are two possible solutions:
1. Factor out the `setTimeout` function
```javascript
var array = [1, 2, 3, 4, 5]

for(var i = 0; i < array.length; i++) {
  delay(i)
}

function delay(i) {
  setTimeout(() => {
    console.log(array[i])
  }, 1000);
}
```
2. Declare the `i` variable in the for loop with the `let` keyword instead of `var`. `let` creates a separate scope for the code block.
```javascript
var array = [1, 2, 3, 4, 5]

for(let i = 0; i < array.length; i++) {
  setTimeout(() => {
    console.log(array[i])
  }, 1000);
}
```

## Promises
We promise to do something, and when the task completes, we either fulfill it or fail to do so. It takes a functions as it's argument, with two parameters - resolve and reject. It has three states: **pending**, **fulfilled**, and **rejected**.

```javascript
const myPromise = new Promise((resolve, reject) => {
  if(condition) {
    resolve('Promise  was fulfilled'); // used when promise succeeded
  } else {
    reject('Promise was rejected'); // used when promise failed
  }
}).then(result => {
  /** Do something with the result.
    * It's executed immediately after your promise is fulfilled with resolve. 
    * result comes from the argument given to the resolve method.
  **/
}).catch(error => {
  /** Used when promise was rejected.
    * It's executed immediately after a promise reject method is called.
    * error is the argument passed into the reject method.
});
```

## Async/Await
Special syntax to work with promises.

__async__ → ensures the function returns a promise, and wraps non-promises in it.\
__await__ → can only be used inside `async` functions, and cannot be used at the top-level. Makes JavaScript wait until that promise settles and returns its result. `await` also accepts *thenables*.

`async/await` also works well with `Promise.all`.

### Error handling
We can use a `try..catch` block to handle errors. If we don't have that, then the promise generated by the call of the async function becomes rejected.

# Error handling - `try..catch`
When an error occurs, due to mistakes, unexpected user input, erroneous server response, etc. the script immediately stops, priting the error the the console. We can use `try..catch` syntax to "catch" errors so that the script knows how to act in the case of an error.
```javascript
const json = "{ bad json }"

try {
  const user = JSON.parse(json)
  // ...
} catch(err) {
  alert('Apologies, the data contain errors. We will try to request it one more time')
  // ...
}
```
1. The `try` block is executed.
2. When an error occurs, its execution stops, and control flows to the beginning of the `catch` block. The `err` variable will contain an error object with details about what happen.
3. If no error occurs, the `catch` block is ignored.

ES2019 introduced optional catch biding, meaning we don't need to write `(err)` if we don't need the error variable.

> __Notes:__ `try..catch` only works for runtime errors. For it to work, the code must be valid JavaScript. Moreover, `try..catch` works synchnonously. So if a exception happens in scheduled code, *e.g.* `setTimeout`, `try..catch` won't catch it. We can get around this by using `try..catch` inside the `setTimout` callback.

## Error object
When an error occurs, JavaScript generates an object containing details about it. The object is then passed as an argument to `catch`. For built-in errors, the Error object contains two main properties:
- `name` → error name. *e.g.* `Reference Error`.
- `message` → textual message about error details.

There are other non-standard properties available in most environments:
- `stack` → current call stack. Used for debugging purposes.

## Custom errors
The `throw` operator is used to generate an error. We can use anything as an error object, but the best practice is to use an object with `name` and `message` properties. JavaScript has many built-in constructors that we can use for standard errors:
- `Error`
- `SyntaxError` → common when we try to `JSON.parse`.
- `ReferenceError` → when we try to execute a function that wasn't declared before.
- `TypeError` → for example, when we declare a variable to be `undefined` and try to execute it like a function.
- `RangeError` → happens with infinite recursion.
- `URIError` → encoding/decoding URIs that are invalid.

```javascript
const json = '{ "age": 30 }' // incomplete data

try {
  const user = JSON.parse(json)
  if(!user.name)
    throw new SyntaxError('Incomplete data: no name')
  
  // ...
} catch(e) {
  alert(`JSON Error: ${e.message}`)  
}
```

## Rethrowing
By its nature, `catch` gets **all** errors from `try`, even if they are non-related. To avoid problems, we can use the rethrowing technique: **“Catch should only process errors that it knows and rethrow all others”**.
1. Catch all errors.
2. In the `catch` block we analyze the error object. To analyze the error type we usually can use `instanceof`.
3. If we don't know how to handle it, we do `throw err`.

```javascript
const json = '{ "age": 30 }' // incomplete data

try {
  const user = JSON.parse(json)
  if(!user.name)
    throw new SyntaxError('Incomplete data: no name')
  
  stuff() //unexpected error
  // ...
} catch(e) {
  if(e instanceof SyntaxError) {
    alert(`JSON Error: ${e.message}`)  
  } else {
    throw e
  }
}
```
The rethrown error will be catched by an outer `try..catch` block, or it will kill the script.

## `try..catch..finally`
The `finally` block runs in all cases, both with errors or no errors. It's often used to finalize something we had started doing independently of the outcome.
```javascript
try {
  // ...
} catch(e) {
  // ...
} finally {
  // ...
}
```
The `finally` clause works for any exit from `try..catch`. That includes an explicit `return` inside the `try` block. The `finally` code is executed, and then the value is returned.

We can also use `finally` without the `catch` clause. Can be useful for whenever we don't want to handle errors there, but want to make sure the processes we'd started are finalized.

## Global catch
> __Warning:__ this is not part of the core JavaScript, and it's environment-specific.

In the case of an uncaught error, usually environments provide some kind of global catch: Node.js has `process.on('uncaughtException')`, and in the browser we can assign a function to the `window.onerror` property.
```javascript
window.onerror = function(message, url, line, col, error) {
  alert(`${message}\nAt ${line}:${col} of ${url}`)
}
```
- `message` → error message.
- `url` → the script's URL where the error happened.
- `line`, `col` → line and column numbers where the error happened.
- `error` → Error object

This global handler's role is usually not to recover the script execution, but to send the error message to developers. There are web-services that provide error-loggin for such cases, *e.g.* [Errorception](https://errorception.com/) and [Muscula](https://www.muscula.com/).

# Importing & Exporting Modules
_Import a module:_
```javascript
import { function1, function2, ... } from './file.js';
```

_Import the module as an object containing all exports:_
```javascript
import * as myModule from './file.js';
```

_Export a module:_
```javascript
export const function1 = function(a, b) { return a + b }
export const function2 = function(a, b) { return a - b }

// OR

export { function1, function2, ... }
```

## Default export
`export default` → used if only one value is being exported from a file or to create a fallback value for a file or module. Can't be used with `var`, `let`, or `const`.
```javascript
export default function Editor() {
  ...
}
```

_Import a default export:_
```javascript
import Editor from './Editor.js';
```

# Sources
[freeCodeCamp](https://freecodecamp.org/)\
[Scheduling: setTimout and setInterval - JavaScript.info](https://javascript.info/settimeout-setinterval)\
[MDN web docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/)\
[Watch Out When Using SetTimeout() in For Loop #JS – Medium](https://medium.com/@axionoso/watch-out-when-using-settimeout-in-for-loop-js-75a047e27a5f)\
[Functions. A Fool's Guide to Writing Functional JS (Part 2) – DEV](https://dev.to/fa7ad/part-2-functions-a-fool-s-guide-to-writing-functional-js-4p5f)\
[The Difference Between Regular Functions and Arrow Functions – Medium](https://medium.com/better-programming/difference-between-regular-functions-and-arrow-functions-f65639aba256)\
[Function as First-Class Objects in JavaScript: Why Does This Matter? – DevelopIntelligence](https://www.developintelligence.com/blog/2016/10/javascript-functions-as-first-class-objects/)\
[How to use the apply(?), call(?), and bind(➰) methods in JavaScript – FreeCodeCamp Blog](https://www.freecodecamp.org/news/how-to-use-the-apply-call-and-bind-methods-in-javascript-80a8e6096a90/)\
[Error handling, "try..catch" – JavaScript.info](https://javascript.info/try-catch)\
[JavaScript Try Catch & Error Handling ES6 Tutorial (2020) – CodingSrc Youtube](https://www.youtube.com/watch?v=ye-aIwGJKNg)\
[Recursion in Functonal JavaScript – sitepoint](https://www.sitepoint.com/recursion-functional-javascript/)\
[Demystifying JavaScript Variable Scope and Hoisting – sitepoint](https://www.sitepoint.com/demystifying-javascript-variable-scope-hoisting/)\
[JavaScript Closures – TutorialRepublic](https://www.tutorialrepublic.com/javascript-tutorial/javascript-closures.php)\
[Learn JavaScript Closures in 6 Minutes – FreeCodeCamp](https://www.freecodecamp.org/news/learn-javascript-closures-in-n-minutes/)
