# Componnent Life Cycle
When we start developing in React, every Component follows a cycle from when it’s created and mounted on the DOM to when it is unmounted and destroyed. This is what we refer to as the Component lifecycle. React provides hooks, methods that get called automatically at each point in the lifecycle, that give you good control of what happens at the point it is invoked. A good understanding of these hooks will give you the power to effectively control and manipulate what goes on in a component throughout its lifetime.

Our lifecycle is broadly categorized into three parts: Mounting, Updating and Unmounting. I will discuss each of these methods and how they can be used.

## Mounting Methods
A component mounts when it is created and first inserted into the DOM i.e when it is rendered for the first time. The methods that are available during this period are:

* constructor()
* componentWillMount()
* render()
* componentDidMount()

###  ComponentWillMount() 
The componentWillMount method is called right before a component mounts or the render method is called. The truth is that you might hardly make use of this method in your React application. Let me explain why.

The componentWillMount method sits between the constructor method and the render method which puts it in a very odd position. Since it’s before the render method, it can be used to set the default configuration for a component, but this is mostly done using the constructor method. And since nothing changes between these two methods, there will be no need to set the configuration again.

Also, the render method has not been called at this point so nothing can be done with the DOM of the component since it has not been mounted. Some might think that this is the right place to make API calls for client-side rendering but this should not be done. API calls are asynchronous and the data might not be returned before the render method gets called. This means that the component might render with empty data at least once.
An example of componnentWillMount includes:
```javascript
   class Example extends React.Component {
        componentWillMount() {
            console.log('Hello Class');
        }

        render() {
            return <h1>Hello world</h1>;
        }
    }

```

###  ComponentDidMount()
This method is available after the component has mounted. That is after the HTML from render has finished loading. It is called once in the component life cycle and it signals that the component and all its sub-components have rendered properly.

This is the best place to make API calls since, at this point, the component has been mounted and is available to the DOM. Generally, componentDidMount is a good place to do all the setup you couldn’t have done without the DOM.
An example of ComponentDidMount includes:
```javascript
class Example extends React.Component {
        componentDidMount() {
            fetch(url).then(results => {
                // The result can be used to serve its purpose
            })
        }
    }

```

This whole week we have been trying to familazrize ourselve with CreateClass Components.
The createClass method provided developers with a factory method to create React class components without using a JavaScript class. It was the status quo for creating React components prior JavaScript ES6, because in JavaScript ES5 there was no class syntax available.
An example of codes include:

```javascript (React classComponent)
var App = React.createClass({
  getInitialState: function() {
    return {
      value: '',
    };
  },
  onChange: function(event) {
    this.setState({ value: event.target.value });
  },
  render: function() {
    return (
      <div>
        <h1>Hello React "createClass" Component!</h1>
        <input
          value={this.state.value}
          type="text"
          onChange={this.onChange}
        />
        <p>{this.state.value}</p>
      </div>
    );
  },
});
```

The createClass() factory method receives an object which defines methods for the React component. Whereas the getInitialState() function is used to set an initial state for the React component, the mandatory render() method is there to display the output with JSX. Additional "methods" (e.g. onChange()) are added by passing more functions to the object.

Lifecycle methods for side-effects are available as well. For instance, in order to write every time the value from the input field to the browser's local storage, we could make use of the componentDidUpdate() lifecycle method by passing a function to the object with an object key named after a React lifecycle method. In addition, the value can be read from the local storage when the component receives its initial state

```javascript
var App = React.createClass({
  getInitialState: function() {
    return {
      value: localStorage.getItem('myValueInLocalStorage') || '',
    };
  },
  componentDidUpdate: function() {
    localStorage.setItem('myValueInLocalStorage', this.state.value);
  },
  onChange: function(event) {
    this.setState({ value: event.target.value });
  },
  render: function() {
    return (
      <div>
        <h1>Hello React "createClass" Component!</h1>
        <input
          value={this.state.value}
          type="text"
          onChange={this.onChange}
        />
        <p>{this.state.value}</p>
      </div>
    );
  },
});
```

## Updating Method
Components do not always remain in the same state after mounting. Sometimes the underlying props could change and the component has to be re-rendered. The updating lifecycle methods give you control over when and how this updating should take place.

There are five updating lifecycle methods and they are called in the order they appear below:

* componentWillReceiveProps
* shouldComponentUpdate
* componentWillUpdate
* render
* componentDidUpdate

### componentWillReceiveProps()
Props are externally passed into a component by its parent component. Sometimes these props are hooked to the state of the parent component. So if the state of the parent component changes, the props passed to the component changes and it has to be updated. If the props are tied to the state of the component, a change in it will mean a change in the state of the component.

componentWillReceiveProps is a method that is called before a component does anything with the new props. This method is called with the new props passed as an argument. Here, we have access to the next set of props and the present ones. Therefore, using this method, we can compare the present props with the new ones and check if anything has really changed.
An example of componentWillReceiveProps includes:
```javascript
 class Example extends React.Component {
      constructor(props) {
        super(props);
        this.state = {number: this.props.number};
      }

      componentWillReceiveProps(nextProps) {
        if (this.props.number !== nextProps.number) {
          this.setState({number: nextProps.number});
        }
      }
```

### shouldComponentUpdate()

This method is called before the component re-renders after receiving a new set of props or there’s a new state. We can see that it receives two arguments, the next props, and the next state. The default behavior is for a component to re-render once there’s a change of state of props.

shouldComponentUpdate is used to let React know that a component’s output is not affected by a change of props or state in the component and thus should not re-render. It returns either a true or false value. If it returns true, the component will go ahead and do what it always does, re-render the component. If it returns false then the component will not update. Note that this does not prevent child components from re-rendering when their state changes.
An example of shouldComponentUpdate includes:

```javascript
    class Example extends React.Component {
      [...]

      shouldComponentUpdate(nextProps, nextState) {
        if (this.state.input == nextState.input) {
          return false;
        }
      }

      [...]
    }
```


### componentWillUpdate() method
componentWillUpdate is the method that can be used to perform preparation before re-rendering occurs. You cannot call this.setState in this method.

One major thing that can be done with this method is to interact with things outside of the React architecture. Also, if you need to do any non-React setup before a component renders such as interacting with an API or checking the window size, componentWillUpdate can be used.

The syntax for componentWillUpdate incudes:
```javascript
   class Example extends React.Component {
      [...]

      componentWillUpdate(nextProps, nextState) {
          // Do something here
      }

      [...]
    }
```


### componentDidUpdate() method
componentDidUpdate is called after any rendered HTML has finished loading. It receives two arguments, the props and state of the component before the current updating period began.

componentDidUpdate is the best place to perform an interaction with a non-React environment like the browser or making HTTP requests. This should be done as long as you compare the current props to the previous props to avoid unnecessary network requests.

An example of componentDidUpdate includes:
```javascript
 class Example extends React.Component {
      [...]

      componentDidUpdate(prevProps, prevState) {
        if (this.props.input == prevProps.input) {
          // make ajax calls
          // Perform any other function
        }
      }

      [...]
    }
```


## Unmounting method
Components do not always stay in the DOM. Sometimes they have to be removed due to changes in state or something else. The unmounting method will help us handle the unmounting of components.

### componentWillUnmount() method
ComponentWillUnmount is called right before a component is removed from the DOM. This is where you can perform any cleanups that should be done such as invalidating timers, canceling network requests, removing event listeners or canceling any subscriptions made in componentDidMount.
The syntax includes:
```javascript
    class Example extends React.Component {  
      [...]

      componentWillUnmount() {
          document.removeEventListener("click", SomeFunction);
      }

      [...]
    }
```
### componentDidCatch() method
A component becomes an error boundary if it defines the componentDidCatch method. In this method, this.setState can be called and used to catch an unhandled JavaScript error in a child component tree and display a fallback UI instead of the component that crashed. These errors are caught during rendering, in lifecycle methods, and in constructors of the whole tree below them.
This is to ensure that an error in a child component does not break the whole app.
This method has two parameters. The first is the actual error thrown. The second parameter is an object with a componentStack property containing the component stack trace information. With these parameters, you can set the error info in state and return an appropriate message in its render method or log to a reporting system.
Here’s an example of how this method can be used in error boundaries:
```javascript
class ErrorBoundary extends React.Component {
      constructor(props) {
        super(props);
        this.state = { hasError: false };
      }

      componentDidCatch(error, info) {
        this.setState({hasError: true });
      }

      render() {
        if (this.state.hasError) {
          return <h1> Oops!!! Broken </h1>;
        }

        return this.props.children;
      }
    } 
```