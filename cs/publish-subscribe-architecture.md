__Publish-Subscribe Architecture__ → messaging pattern. Helps to create an abstraction so different system components can communicate without knowing anything about each other's identity. This creates space, time and synchronization decoupling. The three main components in PSA are:
- __Publishers__ → the sender of messages. They do not specify directly to whom the message is to be sent.
- __Event bus / Message broker__ → acts as an intermediary that collects all the messages from publishers and forward them to subscribers based on their interest.
- __Subscribers__ → the ones which the messages are directed to.

## Types of Subscription Model
### Topic-based
- Events are classified in topics (subjects).
- Subscribers receive events related to a particular keyword.
- Messages are grouped based on the topic.

### Content-based
- Events are classified according to the properties of the notifications.
- Subscribers announce their interest by describing to a property of an event (e.g. specify filter, constraints).
- No concept of grouping messages based on topic (no keywords).

### Type-based
It's a subset of the content-based model.
- Events are classified based on the type of objects, thus being able encapsulate attributes and methods.
- Subscribers express interest on an event type by supplying a filter expression that evaluates the attributes during runtime.
- Messages are grouped based on the type of topic/object (same kind of event).

## PSA using JavaScript
A very basic approach on this architecture is to define a function that does something (e.g. update our UI) and then pass it to another portion of the code, where it will be called.

```javascript
let changeListener = null;

export function subscribe(callbackFunction) {
  changeListener = callbackFunction;
}

export function addPlace(latLng) {
  ... // asynchronous code
  if(changeListener) { changeListener(); }
}

... // sidebar.js
import { getPlaces, subscribe } from './dataservice.js';

function renderCities() {
  ...
}

renderCities();
subscribe(renderCities);
```

While sidebar.js is being loaded, it registers `renderCities` function inside the `dataService`. Then `dataService` invokes this function when it needs to. Where the publisher is the service method and the subscriber of the event is the sidebar component.

We can turn `changeListeners` into an array so multiple components can subscribe to it.
```javascript
let changeListeners = [];

export function subscribe(callbackFunction) {
  changeListeners.push(callbackFunction);
}
```
With this, we should write a function that will invoke all the listeners for us.
```javascript
function publish() {
  changeListeners.forEach(changeListener => changeListener())
}

export function addPlace(latLng) {
  ... // asynchroonous code
  publish();
}
```

We can also use subscribers as a method of transporting data. On the publisher, we pass the data to the subscriber function via parameter.
```javascript
function publish(data)
  changeListeners.forEach(changeListener => changeListener(data))
}

export function addPlace(latLng) {
  ... // asynchronous code
  publish(myPlaces);
}

... // sidebar.js
function renderCities(placesArray) {
 ...
}
```

### PSA in Javascript
This architecture is pretty much used everywhere. `element.addEventListener` is the same mechanism: you subscribe your function to a particular event, which is being called when some action is published by an element.

Modern libraries and frameworks also use this architecture: Angular with RxJS, React with state and props management, Redux, etc.

# Sources
[Why every beginner front-end developer should know publish-subscribe pattern? - ITNext](https://itnext.io/why-every-beginner-front-end-developer-should-know-publish-subscribe-pattern-72a12cd68d44)