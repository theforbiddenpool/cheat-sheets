__HelmetJS__ → type of middleware for Express-based applications that automatically sets HTTP headers to prevent sensitive information from unintentionally being passed between the server and client. It includes support form common situtations like Content Security Policy, XSS Filtering, and HTTP Strict Transport Security.\
Each layer of protection can be configured to best fit the project.

We need to mount each middleware introduced bellow using `app.use()`.

_Hide X-Powerd-By header:_
Hackers can exploit known vulnerabilities in Express/Node if they see that our site if powered by Express. `X-Powered-By` header is sent in every request coming from Express by default. We can explicity set the header to something else, to throw people off.
```javascript
helmet.hidePoweredBy({ setTo: 'PHP 4.2.0' })
```

_Mitigate the risk of clickjacking:_
The `X-Frame-Options` header restricts who can put our site in a frame. It has three modes: `DENY`, `SAMEORIGIN`, AND `ALLOW-FROM`.
```javascript
helmet.frameguard({ action: 'deny' })
```

_Mitigate the risk of XSS:_
The basic rule to lower the risk of an XSS attack is: "Never trust user's input". We should always sanitize all the input coming from the outside (forms, GET query urls, POST bodies, etc.) - find and encode potentically dangerous characters, e.g. < >.\
X-XSS-Protection HTTP header is a basic protection. The browser detects a potential inject script using a heuristic filter. If the header is enabled, the browser changes the script code, neutralizing it. It still has limited support.
```javascript
helmet.xssFilter()
```

_Avoid Inferring the Response MIME Type:_
Browsers can use content or MIME sniffing to guess and process different datatypes coming from a response, overriding the Content-Type headers. This can be convenient, but it can also lead to some dangerous attacks.\
We can set the `X-Content-Type-Options` to `nosniff` to instruct the browser to not bypass the provided Content-Type.
```javascript
helmet.noSniff()
```

_Prevent IE from Opening Untrusted HTML:_
Some web applications will serve untrusted HTML for download. Some versions of IE by default open those HTML files in the context of our site, which allows them to do bad things in the context of our page.\
We can set the `X-Download-Options` header to `noopen` to prevent this.
```javascript
helment.ieNoOpen()
```

_Ask Browsers to Access Our Site via HTTPS Only:_
By setting the header `Strict-Transport-Security`, we tell the browsers to use HTTPS for the future requests in a specified about of time.\
```javascript
helmet.hsts({ maxAge: <seconds>, force: true })
```
To configure HTTPS on a custom website requires the acquisition of a domain, and a SSL/TSL Certificate.

_Disable DNS Prefetching:_
DNS Prefetching may lead to over-use of the DNS service (if we own a big website, visited by millions of people), privacy issues, or page statistics alteration.\
If we have high security needs we can disable it, at the cost of performance.
```javascript
helmet.dnsPrefetchControl()
```

_Disable Client-Side Caching:_
When updating our website we can (try to) disable caching on client's browser, so the user has the newest version. It can be useful in development too. Only use this option when there is a real need, as it has performance benefits.
```javascript
helmet.noCache()
```

_Set a Content Security Policy:_
Content Security Policy prevents the injection of anything unintended into our page, preventing attacks such as XSS vulnerabilities, undesired tracking, malicious frames, etc. It works by defining a whitelist of trusted content sources. It is not supported by older browsers.\
There are multiple directives available, some being HTML 5 Rocks and KeyCDN.
```javascript
helmet.contentSecurityPolicy({ directives: {
  defaultSrc: ["'self'"],
  scriptSrc: ["'self'", "trusted-cdn.com"]
}})
```
It's important to set the `defaultSrc` directive as a fallback. The fallback applies for most of the unspecified directives. `'self'` is a keyword meaning our own website.

## Configure Helmet using the 'parent' `helmet()` middleware
`app.use(helmet())` will automatically include all the middleware introduced above, except `noCache()`, and `contentSecurityPolicy()`. We can also configure any other middleware individually using a configuration object.
```javascript
app.use(helmet({
  frameguard: {
    action: 'deny'
  },
  contentSecurityPolicy: {
    directives: {
      defaultSrc: ["self"],
      styleSrc: ['style.com'],
    }
  },
  dnsPrefetchControl: false
}))
```

# Keywords
__clickjacking__ → technique of tricking a user into interacting with a page different from what the user thinks it is. Can be done using iframing - a hacker can put a hidden layer over our page, hidden buttons can be used to run bad scripts, etc.\
__Cross-site scripting (XSS)__ → malicious scripts are injected into vulnerable pages, with the purpose of stealing sensiteve data like session cookies, or passwords.\
__HTTP Strict Transport Security (HSTS)__ → web security policy which helps to protect website against protocol downgrade attacks and cookie hijacking.
__DNS prefetching__ → to improve performance, most browsers prefetch DNS records for the links in a page so the destination ip is already known when the user clicks on a link.

# Sources
[freeCodeCamp](https://freecodecamp.org)