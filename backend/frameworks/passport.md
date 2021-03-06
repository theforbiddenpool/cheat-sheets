__Passport__ → authentication middleware for Node.js.

__Express-session__ → session middleware for Express.js. We can use it to save the session id as a cookie in the client, keeping personal account information out of the cookie. With the session id key we can access the session data on the server.

_Require Passpord & express-session:_
```javascript
const passport = require('passport')
const session = require('express-session')
```

_Initialize Passport & express-session:_
```javascript
app.use(session({
  secret: process.env.SESSION_SECRET,
  resave: true,
  saveUninitialized: true
}))

app.use(passport.initialize())
app.use(passport.session())
```
`SESSON_SECRET` must be added to the `.env` file. Its value is used to compute the hash used to encrypt our cookie.

## Serialization
__*__ → allows us to know who's communicated with the server without having to send the authentication data at each request for a new page.

_Serializing a user:_
```javascript
passport.serializeUser((user, done) => {
  done(null, user._id)
})
```
- _args_ → the full user object, and a callback used by Passport.
- _callback's return_ → unique key to identify that user. We can use the user _id generated by MongoDB.

_Deserializing a user:_
```javascript
const ObjectID = require('mongodb').ObjectID

passport.deserializeUser((id, done) => {
  db.collection('users').findOne(
    {_id: new ObjectID(id)},
    (err, doc) => done(null, doc)
  )
})
```
- _args_ → key, and callback.
- _callback's return_ → the users full object.

## Connecting to the database
One of the methods is to keep a persistent connection with the database for the full life-cycle of the app.\
We want to connect to the database then start listening for requests. To accomplish that, we need to encompass your serialization and app listener in the `mongo.connect` function.
```javascript
const mongo = require('mongodb').MongoClient

mongo.connect(process.env.DATABASE, (err, client) => {
  if(err) {
    console.log('Database error: ' + err)
  } else {
    console.log('Successful database connection')

    const db = client.db('<db-name>')

    // serialization and app.listen
  }
})
```

## Strategies
__Strategy__ → way of authenticating a user. We can allow users to login using locally saved information or from third-party providers like Google and Github.

### Local
_Require `passport-local`:_
```javascript
const LocalStrategy = require('passport-local')
```

_Initialize and setup strategy:_
```javascript
passport.use(new LocalStrategy(
  function(username, password, done) {
    /** Define the process to take when we try to authenticate someone locally.
    This can be searching the database for the user, and if the user exists compare the passwords. **/
  }
));
```
_Appling the strategy to the `/login` route:_
```javascript
app.route('/login')
  .get(passport.authenticate('local', { failureRedirect: '/' }), (req, res) => {
    res.redirect('/profile')
  })
```
After the user successfully logges in, it's information will be available through `req.user`.

### GitHub
With a GitHub strategy, we don't need to worry about a username or passwords. The user is sent to GitHub's auth page to authenticate and as long as they are logged in then GitHub returns their profile for us to use.\
You will need to obtain a *Client ID* and *Secret ID*. Go to [OAuth Applications](https://github.com/settings/developers) and register a new application. The *Client* and *Secret IDs* ought not be shared. Common practice is to save them in the `.env` file.

_Initialize and setup strategy:_
```javascript
passport.use(new GitHubStrategy({
  clientID: process.env.GITHUB_CLIENT_ID,
  clientSecret: process.env.GITHUB_CLIENT_SECRET,
  callbackURL: /** Url callback **/
  },
  function(accessToken, refreshToken, profile, cb) {
    console.log(profile);
    
    // Database logic
    // profile contains the user profile
    // cb should be called after the doc is returned from the database
  }
));
```

_Logging in the user:_\
The login route should only call passport to authenticate with `github`. The callback route, defined when we registered the application on Github, is the one which redirects the user to `/profile`.
```javascript
app.route('/auth/github')
  .get(passport.authenticate('github'))

app.route('/auth/github/callback')  
  .get(passport.authenticate('github', { failureRedirect: '/' }), (req, res) => {
  res.redirect('/profile')
})
```

## Ensuring protected routes are only accessable to logged in users
This is done by implementing a middleware which verifies if the user is logged in or not using `req.isAuthenticated()`.
```javascript
function ensureAuthenticated(req, res, next) {
  if(req.isAuthenticated())
    return next()
  
  res.redirect('/')
}
```

Add the middleware to every protected route.
```javascript
app.route('/profile')
  .get(ensureAuthenticated, (req, res) => {
    res.render(process.cwd() + '/views/pug/profile')
  })
```

## Logging a user out
```javascript
app.route('/logout')
  .get((req, res) => {
    req.logout()
    res.redirect('/')
  })
```

## Register a new user
The logic of the registration route should be: check if user already exists > (if not) add new user to the database > authenticate the user > redirect to `/profile`.
```javascript
app.route('/register')
  .post('req, res, next' => {
    db.collection('users').findOne({ username: req.body.username }, (err, user) => {
      if(err) next(err)
      else if(user) res.redirect('/')
      else {
        db.collection('users').insertOne({
          username: req.body.username,
          password: req.body.password // for security reasons, the password should be hashed. See bcrypt.
        }, (err, doc) => {
          if(err) res.redirect('/')
          else next(null, user)
        })
      }
    })
  },
    passport.authenticate('local', { failureRedirect: '/' }), (req, res, next) => { res.redirect('/profile') }
  )
```

# Keywords
__Serialize an object__ → convert an object contents into a small key.
__Deserialize an object__ → convert the key into the original object.

# Sources
[freeCodeCamp](https://freecodecamp.org)