We are supposed to finish the code academy, redux exercise. It seemed complictaed to me. 
I am still trying to get a hang of redux.

Later, today in the class we have been started working on the Flux

# What is flux?
Flux is a pattern for managing how data flows through a React application. As we've seen, the preferred method of working with React components is through passing data from one parent component to it's children components. The Flux pattern makes this model the default method for handling data.

There are three distinct roles for dealing with data in the flux methodology:

* Dispatcher
*Stores
* Views (our components)

The major idea behind Flux is that there is a single-source of truth (the stores) and they can only be updated by triggering actions. The actions are responsible for calling the dispatcher, which the stores can subscribe for changes and update their own data accordingly.

When a dispatch has been triggered, and the store updates, it will emit a change event which the views can rerender accordingly.