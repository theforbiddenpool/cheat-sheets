_Require socket.io, http and sessionStore:_
```javascript
const http = require('http').Server(app)
const sessionStore = new require('express-session').MemoryStore()
const io = require('socket.io')(http)
```

Socket.io works through emitting and listening to events. We use the keyword `on` to listen and `emit` to emit an event.

## Handling new connections
```javascript
// in server.js
io.on('connection', socket => {
  console.log('A user has connected')
})

// in client.js
/*global io*/
const socket = io()
```
We will need to add a CDN for the Socket.IO library in the HTML page. If we are connecting to an external socket hosted not on the same url/server, we will need to specify the link - `io.connect('URL')`.

## Emiting an event
When we emit something from the server, we send an event's name and data to all the connected sockets.
```javascript
io.emit('user count', {/* any data you want to pass */})
```

Afterwards, we need to listen on the client for the event.
```javascript
// in client.js
socket.on('user count', data => {
  console.log(data)
  // update UI if needed
})
```

## Handling a disconnect
Similar to a connection, but we listen for it on each socket.
```javascript
io.on('connection', socket => {
  // connection logic

  socket.on('disconnect', () => {
    // disconnect logic
  })
})
```

## Authentication
Web sockets you don't no request and therefore no user data. One way to solve it is by parsing and decoding the cookie that contains the passport session then deserializing it to obtain the user object. We can use `passport.socketio` for this.
```javascript
const passportSocketIo = require('passport.socketio')

// added before anny existing socket code
io.use(passportSocketIo.authorize({
  cookieParser: cookieParser,
  key:          'express.sid',
  secret:       process.env.SESSION_SECRET,
  store:        sessionStore
}));
```
We can also optionally pass `success` and `fail` with a function that will be called after the authentication process completes. The user object will be accessible as `socket.request.user`.