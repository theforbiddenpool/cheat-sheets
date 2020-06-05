__Chai__ → JavaScript testing library. We can write tests that describe our program's requirements and see if our program meets them.

_Require chai:_
```javascript
const chai = require('chai')
```

## Assertions
```javascript
const assert = chai.assert
```

We can test the result of the assertion against an expected outcome.
```
assert.<method>(valueToBeTested, valueToBeCheckedAgainst[, message])
```

There are different methods we can use with assert:
- `.isNull()` and `.isNotNull()`
- `.isDefined()` and `.isNotDefined()`
- `.isOk()` and `.isNotOk()` → test for a truthy or falsy value;
- `.isTrue()`, `.isNotTrue()`, `.isFalse()`, and `.isNotFalse()` → test for the boolean values true and false;
- `.equal()` and `.notEqual()` → compares using `==`;
- `.strictEqual()` and `.notStrictEqual()` → compares using `===`;
- `.deepEqual()` and `.notDeepEqual()` → asserts if two objects are deep equal. Key order doesn't matter. Array elements position does matter;
- `.isAbove()`, `.isBelow()`, `.isAtMost()`, and `.isAtLeast()` → test if the numbers are greater, less than, less than or equal, or greater than or equal;
- `.approximately(actual, expected, delta[, message])` → asserts that the `actual` is equal `expected`, to within a +/- `delta` range;
- `.isArray()` and `.isNotArray()`
- `.include()` and `.notInclude()` → check if a value is in an array or a string contains it;
- `.isString()` and `.isNotString()`
- `.match()` and `.notMatch()` → check if a value matches a regular expression;
- `.property()` and `.notProperty()` → assert that an object has a given property;
- `.typeOf()` and `.notTypeOf()` → assert that value's type is the given string, e.g. number, string;
- `.instanceOf()` and `.notInstanceOf()` → check if an object is an instance of a constructor;

## Test syntax example
```javascript
suite('Integration tests with chai-http', function() {
  test('Test GET /hello with no name', function() {
    // Testing operations & assertions
    // assert.fail() makes the test fail
  })
})
```

# Chai-HTTP
__*__ → puggling that allows doing HTTP requests.

_Require and use Chai-HTTP:_
```javascript
const server = require('../server') // import the Express app

const chaiHttp = require('chai-http')
chai.use(chaiHttp)
```

_Do a GET request:_
```javascript
test('<test name>', function(done) {
  chai.request(server)
    .get('<route>')
    .end(function(err, res) {
      // res contains the response object
      // do the necessary assertions
      // since this is an asynchronous operation, we need to call done()
      done()
    })
})
```

_Do a PUT request:_
```javascript
test('<test name>', function(done) {
  chai.request(server)
    .put('<route>')
    .send({} /** payload encoded as JSON **/)
    .end(function(err, res) {
      // do the necessary assertions
      done()
    })
})
```

# Zombie.js
__*__ → lightweight browser, totally based on JS.

_Require and Set Up Zombie:_
```javascript
const Browser = require('zombie')
Browser.site = 'example.com'
// OR
// If you are testing from a local environment
Browser.localhost('example.com', (process.env.PORT || 3000))
```

## Test example
```javascript
test('<test name>', function(done) {
  browser
    .fill('surname' 'Polo')
    .pressButton('submit', function() {
      // Assertions
      browser.assert.success() // status is OK 200
      browser.assert.text('span#name', 'Marco')
      browser.assert.element('span#dates', 1) // element exists and their count is 1

      done()
    })

})
```

# Keywords
__Headless browser__ → web browser without graphical interface. Useful for testing web pages.

# Sources
[freeCodeCamp](https://freecodecamp.org)