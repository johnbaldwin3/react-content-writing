## State and Props in React Components

In React, a component is used to organize everything that needs to be displayed (rendered) in the DOM. By using component lifecycle methods, we can exert control over the way things are rendered. Component lifecycle methods all operate on either the props or state of a component. But what does that mean?

The main responsibility of a component is to translate raw data into rich HTML, so together the props and the state make up the raw data that the HTML output derives from.

You could say props + state = the input data for the `render` function of a component.

Simply put, **props are a way of passing data from parent to child. State is for data that changes over time.**

Of course, it's a little more complex than this, so lets dive deeper.

**Common ground**

Before separating props and state, let's also identify where they overlap.

- Both props and state are plain JavaScript objects
- Both props and state changes trigger a render update

**Does this go inside props or state?**

If a component needs to alter one of its attributes at some point in time, that attribute should be part of its state, otherwise it should just be a prop for that component.

### Props

*props* (short for properties) are a component's configuration. They are received from above and immutable as far as the Component receiving them is concerned. Phrased differently, props are are the options of the component.

A component cannot change its props, but it is responsible for putting together the props of its child components.

### State

The *state* starts with a default value when a component mounts, and then undergoes mutations with time (mostly generated from user events). It's a serializable representation of one point in time — a snapshot. Since it's common to pass down callback functions through props, props are not serializable.

A component manages its own state internally, but doesn't change the state of its children. You could say the state is private.

**Should this component have state?**

It's important to remember that *state* is optional. Since state increases complexity and reduces predictability, a component without state is preferable. Even though you clearly can't do without state in an interactive app, you should avoid having too many stateful components.

COMPONENT TYPES

- **Stateless Component** — A stateless component has only props, no state. There's not much going on besides the render() function and all their logic revolves around the props they receive. This makes them very easy to follow (and test for that matter). We sometimes call these *presentational components*.
- **Stateful Component** — A statefull component has both props and state. We also call these state managers. They are in charge of client-server communication, processing data and responding to user events. We sometimes call these *container components*. These sort of logistics should be encapsulated in a moderate number of stateful components, while all visualization and formatting logic should move downstream into as many stateless components as possible.


### Conclusion

Props and state both deal with relating information to the component. Props holds information that is set by the parent component, passed down to its children, and does not change. State holds information that changes over time, and the component has the ability to create, update and use state with the help of lifecycle methods.

#### References

[Lucy Bain](http://lucybain.com/blog/2016/react-state-vs-pros/)
