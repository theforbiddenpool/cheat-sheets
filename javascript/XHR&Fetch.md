# XMLHttpRequest
`const xhr = new XMLHttpRequest()` → creates a new instance of the XMLHttpRequest object.

_Initialize a request:_
```javascript
xhr.open(requestType, url[, isAsynchronousRequest])
```

_Send the request:_
```javascript
xhr.send([body])
```
The `body` argument is the content to be sent on a POST request.

_Set the value of an HTTP request header:_
```javascript
xhr.setRequestHeader(header, value)
```

## Event listeners
_Handle the response:_
```javascript
xhr.onload = function() {
  const data = xhr.response
  // process the response
}
```

_Handle a request state change:_
```javascript
xhr.onreadystatechange = function() {}
```
- `xhr.readyState` = 4 → operation is complete
- `xhr.status` = 201 → successful request

## Examples
### GET method
```javascript
const xhr = new XMLHttpRequest();
xhr.open("GET", url ,true);
xhr.send();
xhr.onload = function(){
  // xhr.responseText to get the response text
};
```

### POST method
```javascript
const xhr = new XMLHttpRequest();
xhr.open('POST', url, true);
xhr.setRequestHeader('Content-Type', 'application/json; charset=UTF-8');
xhr.onreadystatechange = function () {
  if (xhr.readyState === 4 && xhr.status === 201){
    // xhr.response to get the response
  }
};
const body = JSON.stringify({ userName: userName, suffix: ' loves cats!' });
xhr.send(body);
```

# Fetch
`fetch()` method → modern and versatile wrapper around XHR. It works based on Promises. It's not supported by older browsers, but can be polyfilled.

```javascript
let response = await fetch(url[, headers])
```
The default HTTP method used is `GET`.

If the promise is reject if `fetch` is unable to make HTTP-request, e.g. network problems. Abnormal HTTP-statuses (404 or 500) do not cause an error.

## Response methods
`response.status` → HTTP status code, e.g. 200.\
`response.ok` → boolean, `true` if the HTTP code is 200-299.\
`response.headers` → Map-like object, containing the response headers.\
`response.body` → ReadableStream object, is the data returned by the request. It allows you to read the body chunk-by-chunk.

## Parsing the response body
To get the response body, we need to use one of these methods:
- `response.text()` → return as text;
- `response.json()` → parse as JSON;
- `response.formData()` → return as `FormData` object;
- `response.blob()` → return as Blob (binary data with type);
- `response.arrayBuffer()` → return as ArrayBuffer (low-level representation of binary data).

## Request headers
To set a request header, use the `headers` argument.
```javascript
let response = fetch(protectedUrl, {
  headers: {
    Authentication: 'secret'
  }
});
```
There is a list of [forbidden HTTP headers](https://fetch.spec.whatwg.org/#forbidden-header-name) we can't set, as they are exclusively controlled by the browser.

## Examples
### GET method returning JSON
```javascript
let url = 'https://api.github.com/repos/javascript-tutorial/en.javascript.info/commits';

let response = await fetch(url);
let commits = await response.json(); 
alert(commits[0].author.login);
```

### GET method, returning Blob
```javascript
let response = await fetch('/article/fetch/logo-fetch.svg');

let blob = await response.blob();

let img = document.createElement('img');
img.style = 'position:fixed;top:10px;left:10px;width:100px';
document.body.append(img);

img.src = URL.createObjectURL(blob);

setTimeout(() => { // hide after three seconds
  img.remove();
  URL.revokeObjectURL(img.src);
}, 3000);
```

### POST method
```javascript
let user = {
  name: 'John',
  surname: 'Smith'
};

let response = await fetch('/article/fetch/post/user', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json;charset=utf-8'
  },
  body: JSON.stringify(user)
});

let result = await response.json();
alert(result.message);
```
By default, the `Content-Type` header is set to `text/plain`. We need to set the correct JSON headers.

### POST method, sending an image
```javascript
async function submit() {
  let blob = await new Promise(resolve => canvasElem.toBlob(resolve, 'image/png'));
  let response = await fetch('/article/fetch/post/image', {
    method: 'POST',
    body: blob
  });

  // the server responds with confirmation and the image size
  let result = await response.json();
  alert(result.message);
}
```

# Sources
[JavaScript.info](https://javascript.info/fetch)
[FreeCodeCamp](https://freecodecamp.org)
[MDN web docs](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)
