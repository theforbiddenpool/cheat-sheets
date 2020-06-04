# Node.js
__Node.js__ → JavaScript runtime, allows developers to write backend programs in Javascript. Node.js has an LTS version (even numbers), and a experimental one (odd numbers). Some built-in libraries are:
- `http` → acts as a HTTP server.
- `fs` → reads and modifies files.
- `path` → module for working with directiory and file paths.
- `exec` → used to execute commands using the operating system.
- `assert` → checks code against prescribed constrains.

Node comes with three commands:
- __node__ → a command line tool;
- __npm__ → a package manager to install modules;
- __npx__ → used to run a module without installing it.

## Browser APIs vs V8
V8 is the JavaScript engine that powers Chrome. Things like `console.log()`, the `document` object, and `setTimeout()` all belong to the browser API, not the JavaScript itself. Node may have implemented some of these, but they are not part of V8.\
V8 on the other hand, is the syntax itself and things like `Math.random()`, `Promises`, etc. Node.js is just a wrapper around V8, so when we run JavaScript commands it passes them to V8 and then V8 passes the output to Node, which prints it to us.\
You can use Node with other JavaScript engines, however V8 is the default one.

## Node CLI
```
node [options]
```
- `-c`, `--check` → checks the file's syntax without executing.
- `-p` → run the script and print.
- `-r` → inject a module into the the system, before Node executes the script.
- `--experimental-modules` → experimental ES Module support. Used for when you want to run new ES things, like `import` statement.
- `--v8-options` → print V8 command line options.

## Global variables
____dirname__ → root directory\
__process__ → interface between the Node enviroment and the operating system. Used to read and write to the operating system. It contains multiple objects inside it. `process.env` is where you find all the enviroment variables of the operating system.

## Enviroment variables
The environment variables are accessible from the app as `process.env.VAR_NAME`. By convention, the variable names should be uppercase, with words separated by an underscore.\
Node by default has some enviroment variables that you can set a value to change Node's behaviour. Some examples are `NODE_DEBUG` and `NODE_PATH`.

### .env file
The `.env file` is a hidden shell file used to pass enviroment variables to our application. It's used to store data you want to keep private or hidden, like API keys, database URI, and store configuration options.

## `console` API
`console` is a Node API that uses `process.stdout.write` to write output to the Node console. It functions similar to the browser's `console` API.\
`console.dir()` works similar to `console.log()`, but allows specifying options such as `depth`. With the `depth` option, it will only print the an object's properties until the specified depth.

## Node process
Node will only continue to run if it has a reason to run, meaning if it as any asynchronous calls that are listening. If not, the process will just exit. If a function throws an error, Node's process will crash and exit.\
In production, Node by itself is not enough. You have to monitor the process and have a cluster of processes (use the `cluster` built-in module or `pm2` third-party package), so if a process finishes or crashes and exits, another is automatically started.

## Wrapping modules
Everything you write in Node gets wrapped IIFE. When you call a function, you will have access to some default arguments: `exports`, `require`, `module`, `__filename`, and `__dirname`. You have access to these because of the wrapping modules mechanic that Node has. By default, you also always return the `exports` object.

## Watching files for changes in development
There are different packages available that watch for changes in the file and restart Node. One of them is `nodemon`. Instead of running the command-line `node`, you just have to change it for `nodemon`.

# Module dependencies
Everytime you require a file, Node will evaluate and execute it the first time you require it, and then cache it. The second time you require it, Node will just read it from the cache. By requiring a file, we are going to have access to the `exports` object.
```javascript
const index = require('./index.js')
console.log(index) // it will print whatever it was on the exports object
```

The `exports` object is an alias to `module.exports`. To add something to `exports` you just have to add a property to the object:
```javascript
exports.answer = 42
exports.answer2 = 37
```

You can turn `exports` into a function, so everytime you require you can execute that function. It's called delayed execution. You can also have an object with properties that are functions.
```javascript
module.exports = () => { console.log('Hello') }

...
require('./index.js')()
```

### !Note
JavaScript now supports an `import` and `export` module syntax. Most of the packages you'll see will be written with the `require` syntax since it existed since day one on Node, but the way forward should be the `import` syntax. It's still important to really know the `require` syntax, but on newer projects you may use the `import` one.

# `http` library
_Create web server and listen on a port:_
```javascript
import http from 'http'
const sever = http.createServer()
...
sever.listen(3000)
```

When the server gets a request, it will emit an event.
```javascript
server.on('request', (req, res) => {
  // do whatever you need when receiving an request
  // in this, you will need to handle any errors and routes using
  res.write('Hello')
  res.end()
})
```

The `http` library is a very raw API. You don't have any easy way to deal with routes or send files. This is where the Express third-party library comes in.

## HTTP verbs
- `GET` → used when fetching some information, without modifying anything.
- `POST` → default method used to send client data with HTML forms. In REST convention, it's used to send data to create new itemss in the database.

# EventEmitter
Useful when you have a module that emits multiple events. You can emit the same event multiple times. Everything in Node is based around this event emitter logic.

_Emit an event:_
```javascript
import EventEmitter from 'events'
const eventEmitter = new EventEmitter()
eventEmitter.emit('change')
```

_Listen for an event:_
```javascript
eventEmitter.on('change', () => {
  // whatever you want to do when the event is emitted
})
```

# Streams
__Streams__ → data that you get over time, not available all at once. Used when we have huge amounts of data to process. Generally you should always use streams because the data can grow. A good use for streams are files: you should read it and write it as a stream. You don't want to buffer 1GB of data in memory.\
__Chunk__ → a piece of data beloging to a stream.

The `express.js` library uses streams to send data. You can create your own streams using the build-in package `stream`.

# Keywords
__rebel mode__ → you can type code directly onto a console. For example, when you run `node` you enter rebel mode where you can type JavaScript and run it. The browser's console is also in rebel mode.\
__modules__ → small, independent programs\
__routing__ → directs users to the correct page based on their interaction with the aplication\
__middleware__ → functions that intercept route handlers, adding some kind of information\
__REST (REpresentational State Transfer) API__ → allows data exchage in a simple way, without the need for clients to know any detail about the server. The client only needs to know where the resouce is (the URL), and the action it wants to perform on it (the verb). Currently, the preferred data format for moving information around the web is JSON.\
__Multipart/form-data encoding__ → used to upload binary files

# Sources
[freeCodeCamp](https://freecodecamp.org)\
[Youtube - Getting Started with Node.js, by Samer Buna](https://www.youtube.com/watch?v=gG3pytAY2MY)