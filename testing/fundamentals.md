Frontend testing can be divided into 3 categories:
1. __E2E Testing__ → the entire application is tested in real-world scenarios, which includes communication between different components (database, APIs, etc) and in a diversity of browsers. It takes the most time and cost.
2. __Integration Testing__ → testing the interaction between elements of our application, *e.g.* communication between UI and an API.
3. __Unit Testing__ → isolated parts of the code are tested. It's the fastest and cheapest to implement.

[![testing categories pyramid](https://res.cloudinary.com/practicaldev/image/fetch/s--OypgjlFL--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://user-images.githubusercontent.com/15229355/55113335-24fcff00-50df-11e9-87e8-cdd5e0e6ad3f.png)](https://dev.to/christopherkade/introduction-to-front-end-unit-testing-510n "Introduction to Front-End unit testing – Dev.to")

## Unit Testing
```javascript
// 1. Method to be tested
function add(x, y) {
  return x + y
}

// 2. The test suite
describle("add method", () => {
  // 3. The unit test
  it("should return 2", () => {
    // 4. The assertion
    expect(add(1, 1)).toBe(2)
  })
})
```
1. __Method to be tested__ → a great way to know what to test is to go from the ground up looking at an application's components.
2. __Test suite__ → group of unit tests that are related, *e.g.* all tests that concern a specific method. It's role is to make test logs more readable.
3. __Unit test__ → the test itself.
4. __Test assertion__ → compares the given value to an expected one.

A popular framework used for unit testing is Jest. If we used *create-react-app* it should be automatically configured. All test files have a similar format: `*.spec.js` or `*.test.js`.

## End-To-End (E2E) Testing
The purpose of end-to-end testing is testing the whole software for dependencies, data integrity and communication with other sytems, interfaces and databases. It uses actual production like data and test environment to simulate real-time settings. They require a working back-end and database.

### UI Integration Testing
A UI Test it's essentially a script that opens a real browser and interacts with the DOM elements, the same way the real end-user does. Even though they provide higher confidence in our app, they have multiple disavantages:
- slowness, hundreds of UI Tests can take minutes to run;
- high-level feedback, if the submit button doesn't work, what's the bug?;
- they render the whole app.

However, when starting to learn about testing, they can be easier to understand than unit tests and are generally more fun to automate.

Some of the more mature tools to run these type of tests are [Cypress](https://www.cypress.io/) and [TestCafé](https://devexpress.github.io/testcafe/).

# Keywords
__Testing framework__ → allows to easily set up a testing environment and run suites. An example is [Jest](https://jestjs.io/), maintained by a team at Facebook.

__Testing code coverage__ → it represents the percentage of the code being tested. We should keep in mind code coverage doesn't mean we've tested every scenario for a given component, so use it with caution. *create-react-app* uses [Istanbul](https://istanbul.js.org/) to report the code coverage, and we can run it using `npm run test --coverage`.

__Test Driven Development (TDD)__ → the act of first deciding the specifications of our program, formulating a failing test, and only then writing the code to make the test pass.

# Sources
[Introduction to Front-End unit testing – Dev.to](https://dev.to/christopherkade/introduction-to-front-end-unit-testing-510n)\
[New to front-end testing! Start from the top of the pyramid! – ITNext](https://itnext.io/new-to-front-end-testing-start-from-the-top-of-the-pyramid-a0039615353c)
