Today we have been working with Redux. We have been provdied with the website.

https://www.freecodecamp.org/ 

# What is Redux?
Redux is a predictable state container for JavaScript apps.

Redux makes it easy to manage the state of your application. Another way of looking at this – it helps you manage the data you display and how you respond to user actions.

# Creating a new ReactJS based project and adding Redux to it
First things first let’s create a new react app, and start it.

 * create-react-app react-redux-practice
 * cd react-redux-tutorial 
 * npm start

Now, let’s go ahead and add the following Redux packages:

* npm install --save redux react-redux

## redux v4.0.1

* What Redux does in a very general sense, is that it creates a global state for the whole application, that can be accessed by any of our component
* It is a state management library
* We have only one state for our whole app, and not states for each of our components

## react-redux v5.1.1

* This is used so we can access Redux’s data and modify it by sending actions to Redux — actually not Redux, but we’ll get there
* The official docs state: It lets our React components read data from a Redux store, and dispatch actions to the store to update data

### When working with Redux, you will need three main things:

1. actions: these are objects that should have two properties, one describing the type of action, and one describing what should be changed in the app state.
2. reducers: these are functions that implement the behavior of the actions. They change the state of the app, based on the action description and the state change description.
3. store: it brings the actions and reducers together, holding and changing the state for the whole app — there is only one store.

### Windows commands
mkdir src\actions
echo "" > src\actions\startAction.js
echo "" > src\actions\stopAction.js

Now let’s edit the src/actions/startAction.js as follows:
```javascript
export const startAction = {
  type: "rotate",
  payload: true
};
```

### connect()
The connect() function connects a React component to a Redux store.

It provides its connected component with the pieces of the data it needs from the store, and the functions it can use to dispatch actions to the store.

It does not modify the component class passed to it; instead, it returns a new, connected component class that wraps the component you passed in.

```javascript
function connect(mapStateToProps?, mapDispatchToProps?, mergeProps?, options?)
```
The mapStateToProps and mapDispatchToProps deals with your Redux store’s state and dispatch, respectively. state and dispatch will be supplied to your mapStateToProps or mapDispatchToProps functions as the first argument.

The returns of mapStateToProps and mapDispatchToProps are referred to internally as stateProps and dispatchProps, respectively. They will be supplied to mergeProps, if defined, as the first and the second argument, where the third argument will be ownProps. The combined result, commonly referred to as mergedProps, will then be supplied to your connected component.

### connect() Parameters
connect accepts four different parameters, all optional. By convention, they are called:

1. mapStateToProps?: Function
2. mapDispatchToProps?: Function | Object
3. mergeProps?: Function
4. options?: Object

### mapStateToProps?: (state, ownProps?) => Object
If a mapStateToProps function is specified, the new wrapper component will subscribe to Redux store updates. This means that any time the store is updated, mapStateToProps will be called. The results of mapStateToProps must be a plain object, which will be merged into the wrapped component’s props. If you don't want to subscribe to store updates, pass null or undefined in place of mapStateToProps.


### Parameters
1. state: Object
2. ownProps?: Object
A mapStateToProps function takes a maximum of two parameters. The number of declared function parameters (a.k.a. arity) affects when it will be called. This also determines whether the function will receive ownProps.

#### state
If your mapStateToProps function is declared as taking one parameter, it will be called whenever the store state changes, and given the store state as the only parameter.
```javascript
const mapStateToProps = state => ({ todos: state.todos })
```

#### ownProps
If your mapStateToProps function is declared as taking two parameters, it will be called whenever the store state changes or when the wrapper component receives new props (based on shallow equality comparisons). It will be given the store state as the first parameter, and the wrapper component's props as the second parameter.

```javascript
const mapStateToProps = (state, ownProps) => ({
  todo: state.todos[ownProps.id]
})
```

### Returns
Your mapStateToProps functions are expected to return an object. This object, normally referred to as stateProps, will be merged as props to your connected component. If you define mergeProps, it will be supplied as the first parameter to mergeProps.

### mapDispatchToProps?: Object | (dispatch, ownProps?) => Object
mapDispatchToProps, this second parameter to connect() may either be an object, a function, or not supplied.

```javascript
// do not pass `mapDispatchToProps`
connect()(MyComponent)
connect(mapState)(MyComponent)
connect(
  mapState,
  null,
  mergeProps,
  options
)(MyComponent)
```
### Parameters
1. dispatch: Function
2. ownProps?: Object

#### dispatch
If our mapDispatchToProps is declared as a function taking one parameter, it will be given the dispatch of our store.

```javascript
const mapDispatchToProps = dispatch => {
  return {
    // dispatching plain actions
    increment: () => dispatch({ type: 'INCREMENT' }),
    decrement: () => dispatch({ type: 'DECREMENT' }),
    reset: () => dispatch({ type: 'RESET' })
  }
}
```

#### 0wnProps
If your mapDispatchToProps function is declared as taking two parameters, it will be called with dispatch as the first parameter and the props passed to the wrapper component as the second parameter, and will be re-invoked whenever the connected component receives new props.
```javascript
// binds on component re-rendering
;<button onClick={() => this.props.toggleTodo(this.props.todoId)} />

// binds on `props` change
const mapDispatchToProps = (dispatch, ownProps) => {
  toggleTodo: () => dispatch(toggleTodo(ownProps.todoId))
}
```

### Returns
Your mapDispatchToProps functions are expected to return an object. Each fields of the object should be a function, calling which is expected to dispatch an action to the store.

The return of your mapDispatchToProps functions are regarded as dispatchProps. It will be merged as props to your connected component. If you define mergeProps, it will be supplied as the second parameter to mergeProps.

```javascript
const createMyAction = () => ({ type: 'MY_ACTION' })
const mapDispatchToProps = (dispatch, ownProps) => {
  const boundActions = bindActionCreators({ createMyAction }, dispatch)
  return {
    dispatchPlainObject: () => dispatch({ type: 'MY_ACTION' }),
    dispatchActionCreatedByActionCreator: () => dispatch(createMyAction()),
    ...boundActions,
    // you may return dispatch here
    dispatch
  }
}
```

### mergeProps?: (stateProps, dispatchProps, ownProps) => Object

If specified, defines how the final props for your own wrapped component are determined. If you do not provide mergeProps, your wrapped component receives { ...ownProps, ...stateProps, ...dispatchProps } by default.

### Parameters
mergeProps should be specified with maximum of three parameters. They are the result of mapStateToProps(), mapDispatchToProps(), and the wrapper component's props, respectively:

1. stateProps
2. dispatchProps
3. ownProps
The fields in the plain object you return from it will be used as the props for the wrapped component. You may specify this function to select a slice of the state based on props, or to bind action creators to a particular variable from props.

### Returns
The return value of mergeProps is referred to as mergedProps and the fields will be used as the props for the wrapped component.

### options?: Object
```javascript
{
  context?: Object,
  pure?: boolean,
  areStatesEqual?: Function,
  areOwnPropsEqual?: Function,
  areStatePropsEqual?: Function,
  areMergedPropsEqual?: Function,
  forwardRef?: boolean,
}
```
## connect() Returns
The return of connect() is a wrapper function that takes your component and returns a wrapper component with the additional props it injects.

```javascript
import { login, logout } from './actionCreators'

const mapState = state => state.user
const mapDispatch = { login, logout }

// first call: returns a hoc that you can use to wrap any component
const connectUser = connect(
  mapState,
  mapDispatch
)

// second call: returns the wrapper component with mergedProps
// you may use the hoc to enable different components to get the same behavior
const ConnectedUserLogin = connectUser(Login)
const ConnectedUserProfile = connectUser(Profile)
```
In most cases, the wrapper function will be called right away, without being saved in a temporary variable:

```javascript

import { login, logout } from './actionCreators'

const mapState = state => state.user
const mapDispatch = { login, logout }

// call connect to generate the wrapper function, and immediately call
// the wrapper function to generate the final wrapper component.

export default connect(
  mapState,
  mapDispatch
)(Login)
```