There are 23 official patterns from the book *Design Patterns - Elements of Reusable Object-Oriented Software*, considered one of the most influential books on OO theory and software development.

# The Singleton
__Singleton pattern__ → design pattern that restricts the instantiation of a class to one object. It should be immutable by the consuming code, and there should be no dange of instantiating more than one of them. Usually, the goal is to manage global application state:
- source of config settings for a web app;
- anything initiated with an API key, on the client-side;
- store data in memory, on the client-side, *e.g.* stores in Flux.

Before ES6, singletons would be written leveraging closures and IIFEs. Besides being more verbose, it does not give us the immutability we desire without adding more complexity. With ES6, we can leverage modules and `const` variable declaration:
```javascript
const _data = []

const UserStore = {
  add: item => _data.push(item),
  get: id => _data.find(d => d.id === id)
}

Object.freeze(UserStore)
export default UserStore
```

We can also use a class to implement the singleton, which allows us to exploit some benefits of using a traditional class, *e.g.* inheritance.

### Ensuring Immutability and Non-Overridability
An object literal can always be copied by using `Object.assign`. On the class side, the constructor of any instance is available in JavaScript and can be invoked to create new instances. Obviously, this would take some effort from another fellow dev.

If we want to be extra sure that nobody messed with the singleness of our singleton, we can check whether or not we've already instantiated a `UserStore`:
```javascript
class UserStore {
  constructor() {
    if(!UserStore.instance) {
      this._data = []
      UserStore.instance = this
    }

    return UserStore.instance
  }
  // ...
}

const instance = new UserStore()
Object.freeze(instance)

export default instance
```

# Dependency Injection
__Inversion of Control (IoC)__ → removes the direct dependencies from components.\
__Dependency Injection (DI)__ → how instances are passed to components. The dependencies are passed into the contructor functions, instead of being created there.

When we start having hundreds of components with dependencies, if they themselves are creating new instances of their dependencies, we'll start running into problems:
1. The components depend directly on each other. Everything has to be included in the right order for it to work.
2. We cannot develop components in parallel.
3. There's no way to effectively test them without their dependencies. This is especially important for unit tests.

We can apply the *Inversion of Control* pattern with some simple *Dependency Injection*.
```javascript
function Pistons() { /** ... **/ }
function TestPistons() { /** ... **/ }
function Engine(pistons) { /** ... **/ }
function Car(wheels, engine) { /** ... **/ }

const pistons = new Pistons()
const testPistons = new TestPistons()
const wheels = new Wheels()
const engine = new Engine(pistons)
const testEngine = new Engine(testPistons)
const car = new Car(wheels, engine)
car.action()
testEngine.action()
```

However, we still need to create the components in the right order. To solve this problem, we need to bring an **IoC container** to manage the Dependency Injection. There are many types of containers, but typically they work like;
- we get a global instance of the container;
- we register our components with the container;
- we request components from the container, and it handles the dependencies for us.

Using an IoC container solves all the problems stated above, with the added benefit that dependencies are defined in a single place instead of throughout our app. We will also be able to separate our components into different files.

For a more advanced solution to IoC containers, we can take a look at [Angular's dependency injection](https://angular.io/guide/architecture-services).

# Decorator Pattern
__Decorators__ → structural design pattern offering the ability to add non-essential behavior to existing classes dynamically. They aim to promote code reuse. A common reason for their use is when features require a large quantity of distinct types of an object.

The Decorator pattern does not rely on prototypal inheritance. Instead, it works with a single base object and progessively add decorator objects that provide the additional capabilities.
```javascript
function Vehicle(type) {
  this.type = type || 'car'
  this.model = 'default'
}

const truck = new Vehicle('truck')
truck.setColor = function(color) {
  this.model = color
}
truck.setColor('blue')
```

The Decorators can also override the superclass functions we want, while keeping all the other methods and properties intact.
```javascript
function Macbook() {
  this.cost = () => 1000
  this.screenSize = () => 11.6  
}

function Memory(macbook) {
  const v = macbook.cost()
  macbook.cost = () => v + 50
}

function Insurance(macbook) {
  const v = macbook.cost()
  macbook.cost = () => v + 250
}

const mb = new Macbook()
Memory(mb)
Insurance(mb)

console.log(mb.cost()) // output: 1300
console.log(mb.screenSize()) // output: 11.6
```

# Strategy Pattern
An interface is made for a method we have in our base class. This interface will then be used to find the right implementation of that method. The implementation will be decided at runtime, based on the client.

The pattern is useful in situations when we are dealing with methods that have multiple implementations. One common use is with payment processing systems. We want our users to be able to use different payment methods. The strategy design pattern lets us decouple the payment methods from the checkout process.
```javascript
class PaymentMethodStrategy {
  static BankAccount(customerInfo) { /** **/ }
  static BitCoin(customerInfo) { /** **/ }
  static CreditCard(customerInfo) { /** **/ }
  static PayPal(customerInfo) { /** **/ }
}

class Checkout  {
  constructor(strategy = 'CreditCard') {
    this.strategy = PaymentMethodStrategy[strategy]
  }

  changeStrategy(newStrategy) {
    this.strategy = PaymentMethodStrategy[newStrategy]
  }

  //...
}
```
We can also save the default payment method in a config file. We must always provide a fallback value. Within our class, we should also define a way to change payment strategies.

It might feel like we're using an interface, but we don't have to write an implementation for the method on each class. It gives us more flexibility than interfaces.

# Observer Pattern
In the Observer design pattern, we create a one-to-many relationship between a subject and observers. The subject holds all the data and the state of that data. The observers will get said data from the subject when the data has been updated. Anytime the state of the subject changes, all the observers will be notified and updated instantly.

Examples of when we would use this pattern are: sending user notifications, updating filters, and handling subscribers. It is especially common in shopping sites, where we have a bunch of filters that are dependent on the value of a top-level filter.

```javascript
class CategoryDropdown {
  constructor() {
    this.categories = ['appliances', 'doors', 'tools']
    this.subscriber = []
  }

  subscribe(observer) {
    this.subscriber.push(observer)
  }

  onChange(selectedCategory) { // how we send out notifications to all the subscribers
    this.subscriber.forEach(observer => observer.update(selectedCategory))
  }
}

class FilterDropdown { /** **/ }

const categoryDropdown = new CategoryDropdown()
const colorsDropdown = new FilterDropdown('colors')
const priceDropdown = new FilterDropdown('price')

categoryDropdown.subscribe(colorsDropdown)
categoryDropdown.subscribe(priceDropdown)
```
The `update` observer method is the implementation of what we want to do when, in this case, the category changes.

# Sources
[JavaScript Design Patterns: The Sigleton – sitepoint](https://www.sitepoint.com/javascript-design-patterns-singleton/)\
[Dependency Injection in JavaScript 101 – dev.to](https://dev.to/azure/dependency-injection-in-javascript-101-2b1e)\
[The Decorator Pattern – O'Reilly](https://www.oreilly.com/library/view/learning-javascript-design/9781449334840/ch09s14.html)\
[4 Design Patterns You Should Know for Web Development – FreeCodeCamp](https://www.freecodecamp.org/news/4-design-patterns-to-use-in-web-development/)
