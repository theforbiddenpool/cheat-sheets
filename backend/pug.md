__Template engine__ → at runtime, it replaces variables in a template file with actual values supplied by the server. Then it transforms the template into a static HTML file that is sent to the client. This allows displaying variables on the page without needing to make an API call from the client.

__Pug__ → a template engine used with Node.js.

_Set the template engine in Express:_
```javascript
app.set('view engine', 'pug')
```

_Render and send the template:_
```javascript
res.render('<file-path>', {/** variables **/})
```
The file path can be a relative path (relative to views), or an absolute path. It doesn't require a file extension.

# Sources
[freecodecamp.org](https://freecodecamp.org)