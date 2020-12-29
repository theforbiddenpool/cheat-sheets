# Memory management
Some languages, like C, have low-level memory management primitives such as `malloc()` and `free()`. JavaScript allocates memory when things are created and "automatically" frees it up when they are not used anymore, a process called *garbage collection*.

### Memory life cycle
Memory life cycle is pretty much always the same:
1. __Allocate memory__ → the operating system allocated memory for our program to use it. Explicit in low-level languages.
2. __Use memory__ → when the program actually makes use of the previously allocated memory. **Read** and **write** operations take place.
3. __Release memory__ → free the entire memory we don't need anymore. Explicit in low-level languages.

### What is memory?
On a hardware level, computer memory consists of a large number of flip flops. Each flip flop contains a few transistors and is capable of storing one bit. Each flip flop is addressable by a **unique identifier**, so we can read and overwrite them.

Variables and data used by all programs plus the programs' code and the operating system is stored in memory.

There are two different types of memory allocation: **static allocation** and **dynamic allocation**.
Static allocation | Dynamic allocation
--- | ---
Size must be known at compile time | Size may be unknown at compile time
Performed at compile time | Performed at run time
Assigned to the stack | Assigned to the heap
FILO (first-in, last-out) | No particular order of assignment

> Code should never have to depend on what the size of the basic data types is. About 20 year ago, integers were typicaly 2 bytes and now they are 4 bytes.

## In JavaScript
### Allocation
JavaScript does all the fork by itself, alongside declaring values.
```javascript
let n = 374; // allocates memory for a number
let s = 'session'; // allocates memory for a string

function f(a) {
  return a + 3;
} // allocates a function (a callable object)

const d = new Date(); // allocates a Date object
```

### Use
Means reading and writing in the allocated memory. It can be done by reding a vlue of a variable, or passing an argument to a function.

### Release
Most of the memory management issues come at this stage.

High-level languages, including JavaScript, use a piece of software called **garbage collector**. Its job is to track memory allocation and use in order to find when a piece allocated memory is not needed any longer, and then free it.

This is a process of approximation since it's impossible for an algorithm to know truly if a piece of memory is no longer needed. Most garbage collectors work by collecting memory which can no longer be accessed, *e.g.* variables pointing to it are out of scope. However, a variable in scope may be pointing to allocated memory, yet it will never be accessed again.

## Garbage collector
Due to the fact that finding wherther some memory is "not needed anymore" is undecidable, garbage collectors implement a restriction solution to the general problem.

### Reference-counting garbage collection
__Memory reference__ → an object is said to reference another object if the former has an access to the latter.

The simplest garbage collection algorithm collects objects if there are **zero** references pointint to it.

> _Possible problems:_ two objects are created and reference another, creating a cycle. Because each have a reference, the refere-counting garbage collector doesn't consider them for garbage collection.

### Mark-and-sweep algorithm
The algorithm determines whether the object is reachable. It goes through 3 steps:
1. A complete list of all roots (global variables referenced in the code) gets built by the garbage collector.
2. All roots and their children are inspected and marked as active.
3. The garbage collector frees all memory pieces that are not marked as active (everything that couldn't be reached).

As of 2012, all modern browsers ship a mark-and-sweep garbage-collector.

Cycles are no longer a problem, since they are not reference anymore by something reachable from the global object.

### Counter intuitive behavior
Garbage collectors are unpredictable. We can't really tell when a collection will be performed, meaning some programs may use more memory than it's actually needed. Most GC implementations share the common pattern of doing collection passes during allocation. If no allocations are performed, most GC stay iddle.

This behavior may cause higher-than-usual memory usage if allocations are made, most of those elements are marked as unreachable, but no further allocations are performed.

## Memory leaks
__Memory leaks__ → pieces of memory that the application has used in the past and is not needed any longer but has not yet been released. *e.g.* event listeners that aren't removed when we change to another page.

Only developers can make it clear whether a piece of memory can be freed. Certain programming languages provide features that help developers do this, while others expect developers to be completely explicit about it.

### Common JavaScript memory leaks
#### 1. Global variables
```javascript
function foo(arg) {
  bar = 'some text'; // equivalentto window.bar = 'some text';
}
```
When an undeclared variable is referenced, a new variable gets created in the *global* object. We can laso accidentally create a global variable using `this`. We can avoid this by addind `'use strict'`.
Special attention needs to be given to global variables used to temporarily store and process large bits of information. Make sure to **assign it as null or reassign it** once we are done with it.

#### 2. Timers or callbacks that are forgotten
When using observers, we need to make sure we make an explicit catt to remove them once we are done with them. Luckly, most modern browsers will do this job for us: they'll automatically collect the observer handlers once the observed object becomse unreachable.

#### 3. Closures
Once a scope for closures is created for closures in the same parent scope, the scope is shared. This means if we create a closure with a method that isn't used, referencing a private variable, and in that same closure we create another one, the unused method and variable will not be garbage collected.

```javascript
var theThing = null;
var replaceThing = function () {
  var originalThing = theThing;
  var unused = function () {
    if (originalThing) // a reference to 'originalThing'
    console.log("hi");
  };
  
  theThing = {
    longStr: new Array(1000000).join('*'),
    someMethod: function () {
      console.log("message");
    }
  };
};

setInterval(replaceThing, 1000);
```
<small>Example taken from [here](https://blog.sessionstack.com/how-javascript-works-memory-management-how-to-handle-4-common-memory-leaks-3f28b94cfbec)</small>

#### 4. Out of DOM references
When we store DOM nodes inside data structures, we need to update them whenever the DOM node is deleted out of the HTML. Additional consideration has to be taken into account when referencing inner or leaf nodes inside a DOM tree: they will keep a reference to their parent.

# Sources
[How JavaScript works: memory management + how to handle 4 common memory leaks](https://blog.sessionstack.com/how-javascript-works-memory-management-how-to-handle-4-common-memory-leaks-3f28b94cfbec)

# Too Long and Complicated To Put Here
[What Every JavaScript Developer Should Know About Floating Points – modernweb](https://modernweb.com/what-every-javascript-developer-should-know-about-floating-points/)\
[How numbers are encoded in JavaScript – 2ality](https://2ality.com/2012/04/number-encoding.html)
