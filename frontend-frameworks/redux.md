> This needs improvement. The sheet is not good at all if you don't know anything about Redux.

**Redux** is a state management framework. Can be used with different web tecnologies, including React.

There is a single state object that is responsible for the entire state of your application, housed in the Redux store. The Redux store is the single source of truth when it comes to application state. Any time a piece of your app wants to update its state, it must do so through the Redux store.

The methods are available from a Redux object.

_Create the Redux Store:_
```javascript
Redux.createStore(reducerFunction)
```

## Reducer Function
It's responsible for the state modifications that take place in response to actions. The reducer is a pure function that takes state and action, then returns a new state.
- **Args**: state, action
- **Return**: state

> **Tips:** You can use a switch statement to manage different action types.

### Reducer Function & State
State is read-only. So the reducer function must always return a new copy of state and never modify state directly. However <mark>Redux does not enforce state immutability, so you are responsible for it</mark>.

### Reducer Composition
Typically, it is a good practice to create a reducer for each piece of application state when they are distinct in some way (*e.g.* authentication and handling user input).
```javascript
Redux.combineReducers({
  key: reducer,
  ...	
})
```
- **Args**: object in which you define properties which associate keys to specific reducer functions. The name you give to the keys will be used by Redux as the name for the associated piece of state.

## State
Retrieve the current state held in the Redux store.
```javascript
store.getState()
```

## Actions
All state updates are triggered by dispatching actions.

__Action__ → JavaScript object containing information about an action event. It has to have a property called "type", and it can also contain data.
```javascript
let action = { type: 'LOGIN', ... }
```

__Action creators__ → JavaScript function that returns an action. This is what you send to the Redux store.

It's common practice with Redux to assign action types as read-only constants, then reference these constants whenever they are used.

### Dispatching an Action
Dispaches actions to the Redux store.
```javascript
store.dispatch(actionCreator())
store.dispatch({ type: 'LOGIN' })
```

## Store Listener
Allows you to subscribe listener functions to the store, which are called whenever an action is dispatched against the store.
```javascript
store.subscribe(functionCallback)
```

## Handle Asynchronous Actions with Middleware
Redux provides middleware designed to handle asynchronous endpoints, called Redux Thunk middleware.

When creating the store, pass the `applyMiddleware` function.
```javascript
const store = Redux.createStore(reducerFunction, Redux.applyMiddleware(ReduxThunk.default));
```

To create an asynchronous function return a function in the action creator that takes dispatch as an argument. Within it, you can dispatch actions and perform asynchronous requests.
```javascript
function handleAsync() {
  return function(dispatch) {
    //perform requests here
    dispatch(receivedData(data))
  }
}
```

> __Notes:__ it's common practice to dispatch an action before initiating any asynchronous behaviour so that the application state knows some data is being requested.

# React Redux App
The state and the dispatch function is available through `this.props`. For simple apps you can just use React, but as the app grows and becames more complex, so does your state management. This is the problem Redux solves.

You create a sigle Redux store that manages the state of your entire app. Your React components subscribe to only the pieces of data in the store that are relevant to their role. Then, you dispatch actions directly from React components, which then trigger store updates. There are exceptions when individual components may have local state specific only to them.

You need to use the `react-redux` package, because Redux is not designed to work with React out of the box. It provides a way for you to pass Redux state and dispatch to your React components as props.

## Provider
Is a wrapper component from React Redux that wraps your React app. Allows you to access the Redux store and dispatch functions throughout your component tree.
```javascript
const Provider = ReactRedux.Provider;
<Provider store={store}>
  <App/>
</Provider>
```

You must specify what state and actions you want. Two functions to accomplish this:
-	`mapStateToProps()` → behind the scenes, React Redux uses the `store.subscribe()` method to implement `mapStateToProps()`.\
	**args**: state\
	**return**: object { messages: state }

-	`mapDispatchToProps()`\
  **args**: dispatch\
	**return**: object `{ prop-name: function() { dispatch(actionFunction()) } }`

## Connect
```javascript
const connect = ReactRedux.connect;
```
- **args**: optional. `mapStateToProps()`, `mapDispatchToProps()`

The arguments are are optional because you may have a compoment that only needs access to state but doesn't need to dispatch any actions, or vice versa. To omit, pass null in its place.

```javascript
const ConnectedComponent = 
  connect(mapStateToProps, mapDispatchToProps)(MyComponent)
```

## Component Naming Conventions
`Presentation` → generally refers to React components that are not directly connected to Redux. They are simply responsible for the presentation of UI.

`Container` → typically resposible for dispatching actions to ther store and often pass store state to child components as props. Created as constants with the `connect()` function.

# Setting Up React-Redux
Similar to when working with plain React, there are some `import` statements needed to make the app work:
```javascript
import React from 'react'
import ReactDOM from 'react-dom'
import { Provider, connect } from 'react-redux'
import { createStore, combineReducers, applyMiddleware } from 'redux'
import thunk from 'redux-thunk'
```

You can also use the [Create React App](https://github.com/facebookincubator/create-react-app) as previously stated in the [React.md sheet](./react.md)

# Sources
[freeCodeCamp](https://freecodecamp.org)