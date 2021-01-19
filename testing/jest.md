On the `scripts` object in the *package.json* file, we can run jest by adding:
```json
"scripts": {
  "test": "jest --watch *.js"
}
```
- `--watch <file-type>` → watch for file changes.

### Basic Test
```javascript
const dbMock = ['string', 'dog', 'cat', 'doggo']

describe('db search', () => {
  it('is searching database', () => {
    expect(dbSearch('test', dbMock)).toEqual([])
    expect(dbSearch('dog', dbMock)).toEqual(['dog', 'doggo'])
  })

  it('work with undefined and null input', () => {
    expect(dbSearch(undefined, dbMock)).toEqual([])
    expect(dbSearch(null, dbMock)).toEqual([])
  })
})
```
`describe` groups similar tests together, while `it` is the individual test itself.

In real life, we don't want to have to request data from the database everytime we run tests. The simplest way to mock the data is by creating an array with some mock data and use that as the result.

We don't need to worry much about the DRY (Don't Repeat Yourself) principle when it comes to tests, since they are never going to be shipped to production. It can even be useful to have verbose tests.

It's good practice to start with a failing test, and only then change it to a successful test. **Just because a test passes, doesn't mean it works.**

### Asynchronous Tests
A good way to check if there are assertions running in a test, especially with asynchronous code is by using:
```javascript
expect.assertions(1)
```

There are two ways to deal with asynchronous:
1. passing the `done` callback.
```javascript
it('calls swapi to get people', (done) => {
  swapi.getPeople(fetch).then(data => {
    expect(data.count).toEqual(87)
    done()
  })
})
```
2. by returning the promise.
```javascript
it('calls swapi to get people', () => {
  return swapi.getPeople(fetch).then(data => {
    expect(data.count).toEqual(87)
  })
})
```

## Mocks and Spies
If we had to wait for every asynchronous call we have, tests would take longer and longer. This is where Mocks come into play - we can fake a function and pretend to have it running.

We can also spy on the behaviour of the mock function we created.
```javascript
it('getPeople returns count and results', () => {
  const mockFetch = jest.fn()
    .mockReturnValue(Promise.resolve({
      json: () => Promise.resolve({
        count: 87,
        results: [0, 1, 2, 3, 4]
      })
    }))
  
  expect.assertions(2)
  return swapi.getPeople(mockFetch).then(data => {
    expect(mockFetch.mock.calls.length).toBe(1)
    expect(mockFetch).toBeCalledWith('https://api.example.com/')

    // other tests
  })
})
```

# Resources
[Jest Cheat Sheet - GitHub](https://github.com/sapegin/jest-cheat-sheet)

# Sources
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie
