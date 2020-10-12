`'use strict'` → enables Strict Mode, which catches common coding mistakes and "unsafe" actions.

__Falsy values__ → value that is considered false when encountered in a boolean context. In JavaScript, these are: `false`, `0`, `-0`, `""` [empty string], `NaN`, `undefined`, and `null`.

# Functions
Arrow function → `() => {}`\
Implicit return with arrow functions → `() => 'value'`

Default parameter → `function greeting(name = 'Anonymous') {}`

## Rest operator
The rest operator (`...`) can be used where multiple parameters are expected.
```javascript
function func1(arg1, arg2, ...args) {
  ...
}
```
The `args` variable will be an array containing all the remaining passed arguments.

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

# Math methods
`Math.random()` → generates random number from 0 to 1 (exclusive).

`Math.floor()` → rounds the number down to its nearest whole number.

`parseInt(str[, radix])` → converts string to number.
- `radix` → specifies the base for the number converted (from 2 [binary] to 36).

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
[Watch Out When Using SetTimeout() in For Loop #JS – Medium](https://medium.com/@axionoso/watch-out-when-using-settimeout-in-for-loop-js-75a047e27a5f)