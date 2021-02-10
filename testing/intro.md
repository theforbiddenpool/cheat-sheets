Frontend testing can be divided into 3 categories:
1. __E2E Testing__ → the entire application is tested in real-world scenarios, which includes communication between different components (database, APIs, etc) and in a diversity of browsers. It takes the most time and cost.
2. __Integration Testing__ → testing the interaction between elements of our application, *e.g.* communication between database and the express app. This is where we would use **mocks** or **spies** to ensure expected side effects, or **subbs** to fake a database call.
3. __Unit Testing__ → isolated parts of the code are tested. It's specificially great when dealing with pure functions. It's the fastest and cheapest to implement. However, they do not test the connection between things.

[![testing categories pyramid](https://res.cloudinary.com/practicaldev/image/fetch/s--OypgjlFL--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://user-images.githubusercontent.com/15229355/55113335-24fcff00-50df-11e9-87e8-cdd5e0e6ad3f.png)](https://dev.to/christopherkade/introduction-to-front-end-unit-testing-510n "Introduction to Front-End unit testing – Dev.to")

Writing tests shouldn't be complicated. We should try to structure our application in a way that writing tests is really simple. This is easily achievable by creating **pure functions**.

## Unit Testing
```javascript
// 1. Method to be tested
function add(x, y) {
  return x + y
}

// 2. The test suite
describe("add method", () => {
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

__Testing library__ → the scaffolding, giving us the ability to use some function calls and some methods for us to write our tests. *e.g.* Jasmine, Jest, Mocha.

__Assertion library__ → provides assertion functions. Both Jasmine and Jest have their own assertion libraries, and Mocha is usually paired with Chai.

__Test Runner__ → allows us to run our tests. *e.g.* Jasmine, Jest, Mocha, Karma. Tests can run in different environments - Karma allows us to run tests in the browser.

__Headless browser__ → stripped down browser usually used to run tests due to better performance. *e.g.* Puppeteer.

__Mock__, __Spies__ and __Stubbing__ → **Spies** provides us informantion about functions, *e.g.* how many times they were called, in what cases, and by who. **Subbing** replaces selected functions with a function to ensure the expected behavior happens. **Mocks** fake a function or a behavior to test different parts of a process. Both Jasmine and Jest have their own verion, and Mocha is often paired with Sinon.js.

__Testing code coverage__ → it represents the percentage of the code being tested. We should keep in mind code coverage doesn't mean we've tested every scenario for a given component, so use it with caution. *e.g.* Instanbul, Jest. To report the code coverage on a *create-react-app*, and we can run `npm run test --coverage`.

__Test Driven Development (TDD)__ → the act of first deciding the specifications of our program, formulating a failing test, and only then writing the code to make the test pass.

__Behavior Driven Development (BDD)__ → describing what a function does, and say what behavior we expect out of it. It's used by the most popular testing frameworks.

# Sources
[Introduction to Front-End unit testing – Dev.to](https://dev.to/christopherkade/introduction-to-front-end-unit-testing-510n)\
[New to front-end testing! Start from the top of the pyramid! – ITNext](https://itnext.io/new-to-front-end-testing-start-from-the-top-of-the-pyramid-a0039615353c)\
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie
