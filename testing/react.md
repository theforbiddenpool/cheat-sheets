__Enzyme__ → JavaScript testing utility for React created by AirBNB. It allows us to render a component, and gives us methods for us to test said component.

```
$ npm i --dev enzyme enzyme-adapter-react-16
```

To setup Enzyme, we need to create a *src/setupTests.js* file.
```javascript
import { configure } from 'enzyme'
import Adapter from 'enzyme-adapter-react-16'

configure({ adapter: new Adapter() })
```

The three available functions to render a React component to later test it are:
- `shallow` → only renders the specified component.
- `mount` → full DOM rendering. Useful for components that interact with the DOM API. It must be run in a browser-like environment.
- `render` → render React components to a static HTML. It will does render it's children components.
Most of the time we'll want to use `shallow`. However, there are certain use cases for the other two.

### `shallow`
Shallow rendering is useful because it forces us to test only one component at a time - a unit.
```javascript
import { shallow } from 'enzyme'
import React from 'react'
import Card from './Card'

it('expect to render Card component', () => {
  expect(shallow(<Card />).length).toEqual(1)
})
```

## Testing Stateful Components
```javascript
it('corretly increments the counter', () => {
  const mockColor = 'red'
  const wrapper = shallow(<CounterButton color={mockColor}/>)

  expect(wrapper.props().color).toEqual('red')
  wrapper.find('[id="counter"]').simulate('click')
  expect(wrapper.state()).toEqual({ count: 1 })
})
```

## Testing Container Components
A good principle to live by is having each component doing a specific thing. When using Redux, this is especially true. There are multiple ways we can test our connected component:
- `redux-mock-store`;
- export the `App` component without `Connect`;
- move all the non-Redux code to its own file.

Moving non-Redux code to their own file will make the code easier to test.
```javascript
let wrapper

beforeEach(() => {
  const mockProps = {
    onRequestAnimals: jest.fn(),
    animals: [],
  }
  wrapper = shallow(<MainPage {...mockProps} />)
})

it('renders MainPage without craching', () => {
  expect(wrapper).toMatchSnapshot()
})
```

## Testing Individual Methods In a Component
```javascript
it('filters array correctly', () => {
  expect(wrapper.instance().filterArray([])).toEqual([])
})
```

# Snapshot Testing
Instead of keep repeating HTML assertions to check if x element exists on the rendered component, Jest provides us with **Snapshot Testing**. A folder will be created, named *\_\_snapshots\_\_*, containing a snapshot of the component. If we change the html, it will automatically fail the test.
```javascript
it('expect to render Card component', () => {
  expect(shallow(<Card />)).toMatchSnapshop()
})
```

Snapshots also work with stateful components. The *\_\_snaphots\_\_* folder should be uploaded to the remote repo, so all developers have access to it.

#### Updating a Snapshot
When the Snapshot test fails, we have the option of pressing `w`. We can then use the `u` option to update the failing snapshots .

# Redux
## Testing Reducers
Reducers are pure functions, therefore they are quite simple to test.
```javascript
import { CHANGE_SEARCHFIELD } from './constants'
import * as reducers from './reducers'

describe('searchArray reducer', () => {
  it('should return the initial state', () => {
    expect(reducers.searchArray(undefined, {}))
      .toEqual({ searchField: '' })
  })

  it('should handle CHANGE_SEARCHFIELD', () => {
    const initialStateSearch = { searchField: '' }

    expect(reducers.searchArray(initialStateSearch, {
      type: CHANGE_SEARCHFIELD,
      payload: 'abc'
    })).toEqual({ searchField: 'abc' })
  })
})
```

## Testing Actions
Simple actions are easy to test - we just need to use plain Jest. With asynchronous actions, because we need access to the `dispatch` callback, we can use the package `redux-mock-store`.
```javascript
import configureStore from 'redux-mock-store'
import thunkMiddleware from 'redux-thunk'
import * as actions from './actions'

const mockStore = configureStore([thunkMiddleware])

it('handles requesting from the API', () => {
  const store = mockStore()
  store.dispatch(actions.requestFromAPI())
  const expectedAction = {
    type: REQUEST_API_PENDING,
  }
  expect(action[0]).toEqual(expectedAction)
})
```
Most of the times, we'll be adding the mock store in a set up tests file, so all tests have access to it.

# Resources
[nock](https://www.npmjs.com/package/nock) - use to pretend doing an HTTP request\
[supertest](https://www.npmjs.com/package/supertest) - library for testing HTTP requests

# Sources
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie
