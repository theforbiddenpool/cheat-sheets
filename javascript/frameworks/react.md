__React__ → open-source JavaScript library for building user interfaces, created by Facebook. It's use to:
- create components;
- handle state and props;
- update data as it changes using event listeners and lifecycle methods.

We can render elements directly to the HTML DOM using React's rendering API - ReactDOM.
```javascript
ReactDOM.render(componentToRender, targetNode)
```

# JSX
React also allows to write HTML directly within JavaScript, using an extension of JavaScript called **JSX**. JSX is similar to HTML. JSX has to be compiled into JavaScript – Babel is a popular tool.
```javascript
const JSX = (
  <div>
    <p>This is a paragraph. JSX must return only one element, in this case, the parent div.</p>
  <div>
)
```

To write JavaScript within JSX, we do:
```javascript
{ 'write code here' }
```

To write comments, we apply the same principle:
```javascript
{ /* comment here */ }
```

## JSX vs. HTML
1. All HTML attributes and event references become camelCase.\
`class` → `className`\
`onclick` → `onClick`

2. All tags must have a closing tag. Any element can be writing with a self-closing tag.\
`<br />`\
`<div />`\
`<div></div>`\
`<CustomComponent />`

## Inline Styles
We can use a external stylesheet, but we can also use inline styles. That is quite common in React development.

Properties are *camelCase*, and the style attribute has to equal to a JavaScript object. All property value length units are assumed to be `px` unsless otherwise specified. You can use an object to hold the styles.
```jsx
<div style={{ color: "yellow", fontSize: 16 }}>Mellow Yellow</div>
```

# React
## Creating Components
Everything in React is a component.

__Stateless component__ → one that can receive data and render it, but does not manage or track changes to that data.

### Stateless Functional Component
Created by using a JavaScript function that returns either JSX or null. The name must begin with a capital letter.
```javascript
const DemoComponent = () => {
  return (
    <div className='customClass' />
  );
};
```

### ES6 Class Component
Class that extends `React.Component`. The class will have access to many useful React features. It's best practice to call a component's constructor with `super`, and pass props to both.
```javascript
class Kitten extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    // can write JavaScript code here
    return <h1>Hi</h1>;
  }
}
```

## Composition
Separating the UI code from the code responsible for handling the app logic is helpful. You can break down your UI into its basic bulding blocks, and those pieces become the components.

To compose these components together, you need to create an parent component, which renders each of those components. For that, you need to use a custom HTML tag in the JSX with the same name as each component.
```javascript
return (
  <App>
    <Navbar />
    <Dashboard />
    <Footer />
  </App>
)
```

## Props
You can pass properties to child components.

_Passing the custom value:_
```javascript
<App>
  <Welcome user='Mark' />
</App>
```

_To access this value:_
```javascript
// Stateless Functional Component
const Welcome = (props) => <h1>Hello, {props.user}</h1>

// OR

// ES6 Class Component
{ this.props.propName }
```

_Using Default Props:_
```javascript
MyComponent.defaultProps = { propName: 'default value of the prop' }
```
The default prop value is only used if other isn't specified.

_Defining the Props you expect:_
```javascript
MyComponent.propTypes = { propName: PropTypes.func.isRequired }
```
- `func` → checks if the prop is an function. Only function (`func`) and boolean (`bool`) use unusual spelling. There are other types available.
- `isRequired` → tells React the Prop is required

> _Note:_ As of React v15.5.0, PropTypes is imported independently from React (`import PropTypes form 'prop-types';`).

## State
State consists of any data your application needs to know about, that can change over time. It allows you to track important data in your app and render a UI in response to changes in this data. The state object can be as complex or as simple as you need it to be.

When the state data updates, it triggers a re-render of the component using that data. React updates the actual DOM, but only where necessary.

_Creating a stateful compoment:_
Declare a state property in the component's constructor. The state property must be set to a JavaScript object.
```javascript
constructor(props) {
  super(props)
  this.state = { /* state */ }
}
```

_Access state data:_
```javascript
{ this.state.propName }
```

_Setting the state value:_
```javascript
this.setState({ username: 'Lewis' })
```
It's done by using `this.setState()`, passing in an object with key-value pairs. React may batch multiple updates in order to improve performance, meaning state updates using this method can be asynchronous. There is an alternative syntax in order to avoid this.

### Knowing the Previous State
Because the state update may be asynchronous, `this.state` is not reliable to get the previous value. So you pass arguments with setState:
```javascript
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```
`props` argument is opcional, if you don't need it you can only pass state.

### Pass State as Props to Child Components
A commom pattern is to have a stateful component containing the state important to your app, that then renders child components. You only pass the information important to that child component.

This shows two important paradigms in React:
- unidirectional data flow;
- complex stateful apps can be broken down into just a few, or maybe a single, stateful component.

## Lifecycle Methods
__Lifecycle methods__, or __lifecycle hooks__ → special methods that allow you to perform actions at certain points in time.

### `componentWillMount()`
> __Note:__ will be deprecated in future version 16.X and removed in version 17.

Called before the `render()` method when a component is being mounted to the DOM.

### `componentDidMount()`
Called after a component is mounted to the DOM. This is where you should place API calls or any calls to your server. Any calls to `setState()` here will trigger a re-rendering of the component. Also the best place to attach any event listeners you need to add for specific functionality.

> __Note:__ React provides a synthetic event system which wraps the native event system present in browsers. It's great for most interactions you'll manage on DOM elements. However, if you want to attach an event handler to the document or window objects, you have to do this directly.

### `shouldComponentUpdate()`
Called when child components receive new state or props. You can declare specifically if components should update or not. It's a useful way to optimize performance.
- __Args__: `nextProps`, `nextState`
- __Return__: `boolean`, tells React if component should update or not

### `componentDidUpdate()`, `componentWillUnmount()`
It's good practice to use this method to clean up on React components before they are unmounted and destroyed. Removing event listeners is an example.

## Conditionally Render Elements
```javascript
{ condition && <p>markup</p> }
```
If the condition is true the markup will be returned. If the condition is false, the operation will immediately return false and return nothing. It allows you to handle complex conditional logic in your `render()` method without repeating a lot of code.

Ternary expressions can also be used.
```javascript
condition ? expressionIfTrue : expressionIfFalse
```

Because of the way JSX is compiled, if/else statements can't be inserted directly into JSX code. You have to used them outside of the return statement.

## Render React on The Server with `renderToString`
You can run JavaScript on a Node server, therefore you can also run React code. Without doing this, the app would consist of a relatively empty HTML file and a large bundle of JavaScript when it's initially loaded to the browser.
- This is not ideal to search engines trying to index the content of your page,
- By doing it, creates a faster initial page load experience.

React will still be able to recognize your app and manage it after the inital load.
```javascript
ReactDOMServer.renderToString(<App />)
```

## React Hooks
**Hooks** are a new addition in React 16.8. They let us use state and other React features without writing a class.

__useNameHook__ → the standard is to name the hook with use + name of the component

React already comes with some built-in hoooks. Some you may encounter are:
- `useState` → returns a stateful value, and a function to update it.
- `useEffect` → accepts a funcction that contains imperative, possibly effectful code.
- `useContext` → accepts a context object and returns the current context value for that context.

Check the [React.js Docs](https://reactjs.org/docs/hooks-intro.html) for more information on hooks.


# Setting Up React
If you are working with npm and a file system on your own machine the code, there's is some import statements needed to make React work:
```javascript
import React from 'react'
import ReactDOM from 'react-dom'
```

Writing React and Redux code generally requires some configuration. If you are interestend in experimenting on your own machine, the [Create React App](https://github.com/facebookincubator/create-react-app) comes configuerd and ready to go.

Alternively you can enable [Babel](https://babeljs.io/) as a JavaScript Preprocessor in [CodePen](https://codepen.io/), add React and ReactDOM as external JavaScript resourses, and work there as well.

# Resources
- [why-did-you-update – GitHub](https://github.com/welldone-software/why-did-you-render) → patches React to notify us about avoidable re-renders.

# Sources
[freeCodeCamp](https://freecodecamp.org/)\
[Hooks API Reference - React.js Docs](https://reactjs.org/docs/hooks-reference.html)