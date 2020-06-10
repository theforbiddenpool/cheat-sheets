# Express.js
__Express__ → an Node.js module, used as an alternative to the `http` build-in module. It runs between the server created by Node.js and the front-end pages of a web application. Also handles an application's routing.

_Start an Express app object_:
```javascript
const express = require('express')
const app = express()
```

All the coude you may want to add goes between the `app` object and the `app.listen()` method.

# Routes
`app.<method>(<path>, <handler>)`
  - `method` → an http method, such as `get` or `post`.
  - `path` → relative path on the server (string or regex).
  - `handler` → function called when the route is matched. Takes the form `function(req, res){}`, where `req` is the request object and `res` is the response one.
```javascript
app.get('/', (req, res) => res.sendFile(__dirname + '/views/index.html))
```

You can also chain different methods on the same route using the following syntax:
```
app.route(<path>)
  .get(<handler>)
  .post(<handler>)
```

__Response object methods:__
- `res.send(<string>)` → serve the specified string.
- `res.sendFile(<path>)` → serve the specified file. This method will set the appropriate headers to instruct the browser on how to handle the file we want to send, according to its type. `path` is an absolute path to the file; it can be calculated using `__dirname + relativePath/file.ext`.
- `res.json(<jsonObject>)` → serve a json object. Converts a valid JavaScript object to a string, setting the appropriate headers to tell the browser we are serving JSON.

## Serving static assets
The application may need some static assets (stylesheets, scripts, images). In Express, this is accomplished by using middleware.

_Set a static path where the files are located:_
```
express.static(<path>)
```
- `path` → absolute path of the folder containing the assets.

_e.g._
```javascript
app.use(express.static(__dirname + '/public'))
```

## Handling missing pages (404)
A common way to handle this is adding a middleware after all the other routes.
```javascript
app.use((req, res, next) => {
  res.status(404)
    .type('text')
    .send('Not Found')
})
```

# Root-level middleware
Function used to execute some code that can have side-effects on the app. Usually adds information to the request or response objects. Can also be used to perform some validation on data. At each point of the middleware stack you can block the execution of the current chain and pass control to functions specifically designed to handle errors.

__Arguments__:
- `req` → request object;
- `res` → response object;
- `next` → function, which corresponds to the next function in the application's request-response cycle.

These functions can also end the cycle by sending a response when some condition is met. If they don't send a response when they are done, the `next()` function must be called, otherwise the application will be stuck forever.

_Mount a middleware_:
```
app.use(<path>, <mware-function>)
```

_Mount a middleware on a specific type of request_:
```
app.<method>(<path>, <mware-function>)
```

_Chain a middleware inside a route definition_:
```javascript
app.get('/user', (req, res, next) => {
  req.user = getTheUserSync() //Hypothetical synchronous operation
  next()
}, (req, res) => res.send(req.user))
```
This is useful to split the server operations into smaller units, leading to a better app structure.

# Parameters
Allows users to communicate to us what they want to get from our service.

## Route parameters
? → named segments on the URL, delimited by slashes (`/`).

Each segment captures the value of the part of the URL which matches its position. The captures values can be found in `req.params` object. If the capture value is to be optional, add a `?` to the end.\
_e.g._
```javascript
app.get('/:word/echo', (req, res) => res.json({ echo: req.params.word }))
app.get('/:date?', (req, res) => res.json({ echo: req.params.date }))
```

## Query parameters
? → data being encoded after the route path. It's delimited by a question mark (`?`), and includes `field=value` couples. Each couple is separated by an ampersand (`&`).

The value can be found in the `req.query` object. Some characters, like the (`%`) cannot be in URLs and have to be encoded in different format before we can send them.\
_e.g._
```javascript
app.get('/name', (req, res) => res.json({ name: req.query.first + ' ' + req.query.last }))
```

## Request body
? → data sent usually by POST. The default format used by HTML forms is a query string, but it can be changed using AJAX into JSON.

The value can be found in the `req.body` object.\
_e.g._
```javascript
app.post('/name', (req, res) => res.json({ name: req.body.first + ' ' + req.body.last }))
```

# body-parser
Allows you to use a series of middleware, which can decode data in different formats.

_Mount the middleware to handle urlencoded data:_
```javascript
app.use(bodyParser.urlencoded({ extend: false }))
```
- `extend` → configuration option that tells the parser to use the classic encoding, only allowing strings or arrays. The extended version allows more data flexibility, but it's outmatched by JSON.

# Sources
[freeCodeCamp](https://freecodecamp.org)