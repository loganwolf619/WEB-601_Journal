## React Components ..

**What are Components?**
They are the main builidng block of an React eleement. A component is a javascript class or funciton that optionaly accepts inputs which could be prps and then returns a React element which describes how the section of the UI should appear.

*An Example of First component includes:*

```
const Greeting = () => <h1>Hello World today!</h1>;
```

**Functional Components:**
- These components are purely presentational and are simply represented by a function that optionally takes props and returns a React element to be rendered to the page.
- It is preferred to use functional components whenever possible because of their predictability and conciseness. Since, they are purely presentational, their output is always the same given the same props.
We may consider functional component to serve these conditions which include:
1. Functional:- Becuase they are basically considered to be functions.
2. Stateless:- Because they do not hold or manage any state
3. Presentational:- Becuase usually they provide output to UI elements.

**Class Components:**
These components are ususally created with the help of ES6's class syntax.
They often have additonal features which has the ability to contain logic, local state, and other capabailities.

1. Class:- They are basically called classes.
2. Smart:-They contain the logic.
3. Stateful:- They can hold and/or manage local state
4. Container:-They usually hold or contain a lrage number of components, mostly functional components.


There are various ways to choose different typ[es of components. However under these certain crieria we are going to use a class component:
- If we need to manage the local state
- If we need to add lifecycle methods to our components
- If we need to add logic for event handlers

**Props**
- Props are React’s way of making components easily and dynamically customisable. They provide a way of passing properties/data down from one component to another, typically from a parent to a child component (unidirectional dataflow).
- Props are read-only and that a component must never modify the props passed to it. As such, when a component is passed props as input, it should always return the same result for the same input.

In the idnex.html, we can run this folloowing scripts in our *index.html* document which might look like this:
```
const Greeting = props => <h1>Hello {props.name}</h1>;
   ReactDOM.render(
     <Greeting name={‘Edmond’}/>,
     document.getElementById('root')
   );
   
```
