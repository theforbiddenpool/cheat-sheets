__Routing__ → the capacity to show different pages to the user. The user can move between different parts of an application by entering a URL or clicking on an element.

_Install React Router_
```
$ npm install react-router-dom
```

[React Router Documentation](https://reacttraining.com/react-router/web/guides/quick-start)

# Basics
## BrowserRouter
This should hold everything in our app where routing is needed.
```javascript
import { BrowserRouter as Router } from 'react-router-dom'
...
(
  <Router>
    <main>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
          <li><a href="/about">About</a></li>
          <li><a href="/contact">Contact</a></li>
        </ul>
      </nav>
    </main>
  </Router>
)
```

## Rendering Routes
**Component**: Route\
**Props**:
- path → the path of the route.
- render → will display the content whenever the route is reached.
- component → the component to display when the route is reached.
- exact → if the path starts with /, React Router will render the component. So the Home component will always appear. exact changes that default behavior, rendering the component only if it matches the full path.
```javascript
import { BrowserRouter as Router, Route } from 'react-router-dom'
...
(
  ...
  <Route path="/" exact render={() => <h1>Welcome!</h1>} />
  <Route path="/about" component={About} />
  <Route path="/contact" component={Contact} />
)
```

## Using Link to switch pages
**Component**: Link\
**Purpose**: be able to switch between pages without reloading it\
**Props**:
- to → the path of the route to go to.
```javascript
import { BrowserRouter as Router, Route, Link } from 'react-router-dom'
(
  ...
  <li><Link to="/">Home</a></li>
  <li><Link to="/about">About</a></li>
  <li><Link to="/contact">Contact</a></li>
  ...
)
```

**Component**: Switch\
**Purpose**: tells React Router to load only one route at a time
```javascript
import { BrowserRouter as Router, Route, Link, Switch } from 'react-router-dom'
(
  ...
  <Switch>
    <Route path="/" exact render={() => <h1>Welcome!</h1>} />
    <Route path="/about" component={About} />
    <Route path="/contact" component={Contact} />
  </Switch>
)
```

## Passing route parameters
```javascript
(
  const name = 'John Doe'
  ...
  <li><Link to={`/about/${name}`}>About</Link></li>
  ...
  <Route path="/about/:name"  component={About} />
)

const About = ({match:{params:{name}}}) => (
  // props.match.params.name
  <Fragment>
    <h1>About {name}</h1>
    <FakeText />
  </Fragment>
);
```

## Navigating programmatically
The props we receive have some convenient methods we can use to navigate between pages.

**Props object**: history\
**Methods**:
- push → pushes a new entry onto the history stack, changing the displaying page. history.push('/')
- replace → mimics the behavior of Redirect component.
- goBack
- goForward

## Redirecting to another page
**Component**: Redirect
**Purpose**: redirect the user to another page
Props:
- to → the route to go to

### Redirecting to a 404 page
Create a Route component to show it. The route will catch every bath that doesn't exist and redirect the user to the 404 page.
```javascript
<Route render={() => <h1>404: page not found</h1>} />
```

## Guarding routes
There are many ways to protect routes to React. You can do it by using an ternary operator to render the routes if the condition is true, otherwise redirect to another page.
```javascript
<Switch>
  <Route path="/" exact component={Home} />
  { isAuthenticated ? 
    <>
    <Route path="/about/:name"  component={About} />
    <Route path="/contact"  component={Contact} />
    </> 
    : <Redirect to="/" />
  }      
</Switch>
```

# Router Hooks
__useHistory__ → gives us access to the history instance without pulling it from props.\
__useParams__ → help us get the parameter passed on the URL without using the props object.\
__useLocation__ → returns the location object that represents the current URL.

# Sources
[A Complete Beginner's Guide to React Router (Including Router Hooks) - freeCodeCamp](https://www.freecodecamp.org/news/a-complete-beginners-guide-to-react-router-include-router-hooks/)