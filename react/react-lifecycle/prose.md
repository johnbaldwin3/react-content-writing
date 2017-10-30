## Lifecycle of a React component

As you have been learning, in React you use **components** to organize everything that needs to be displayed. Most JavaScript view libraries and frameworks re-render the entirety of the application any time any state changes. This is similar to doing a full page refresh. React only re-renders the components necessary to the new state of the application.

Because components are constantly being re-rendered, there will be times when you want to do something before or after a component has rendered, or may want to avoid a re-render. This is where the component *lifecycle* comes into play. The **component lifecycle** describes the process of stages that every React component goes through. To understand these stages, you first to need understand the way React renders with a **virtual DOM**.

### React DOM

![React-DOM.png](https://tiy-learn-content.s3.amazonaws.com/c5bddec8-React-DOM.png)

React creates a **virtual DOM** by abstracting the **application DOM** and maintaining it in memory. React uses this Virtual DOM to handle in-page interactions and updates from the server. With that input, React then compares the *new state* of the Virtual DOM with the *previous state* of the Virtual DOM and updates the **physical DOM** with the changed elements. So the physical DOM always reflects the up-to-date application state.

### Component Lifecycle Methods

In order to have more control over the stages the component is going through, React provides *methods* that denote when the different stages occur. These are called **component lifecycle methods** and proceed in a certain order. There are three major steps that the stages go through: mounting, updating and unmounting.

#### Mounting

Mounting is when the component is created (initialized) and then inserted into the DOM.

The following component lifecycle methods can be called in relation to component mounting.

- `constructor`
  - Called before the component is mounted. This is the place to initialize state and bind methods.
- `componentWillMount`
  - invoked immediately before mounting occurs (before render).  
  - **Use case:** App configuration in the root component.
  - **Should I call setState?:** Yes, but use default state, instead.

- `render`
  - The `render` method is required on a component, and it must return a *single React element* (either a native DOM component `<div />` or composite component you have defined). The `render` method should not modify the state.
- `componentDidMount`
  - invoked immediately after a component is mounted.
  - **Use case:** Loading data, i.e., `fetch` or AJAX calls.
  - **Should I call setState?:** Yes.


#### Updating

A component is re-rendered because a props or state change occurs.

The following component lifecycle methods can be called when addressing changes.

- `componentWillReceiveProps`
  - invoked before a mounted component receives new props. Use this method if you need to update the state in response to prop changes.
  - **Use case:** Triggering state transitions on prop changes.
  - **Should I call setState?:** Yes.
- `shouldComponentUpdate`
  - invoked before rendering, when new props or state are being received. This method allows your component to exit the lifecycle and avoid unnecessary re-rendering. Useful when only a small amount of data has changed, if there is no update the component and all of its children will break from the lifecyle and the most recent virtual DOM from this component downward will persist.
  - **Use case:** Controlling when the component renders.
  - **Should I call setState?:** No.
- `componentWillUpdate`
  - invoked immediately before rendering when new props or state are being received
  - **Use case:** Used on a component that has `shouldComponentUpdate`. (use it instead of `componentWillUpdate`). Note: no access to previous props.
  - **Should I call setState?:** No.
- `render`
- `componentDidUpdate`
  - invoked immediately after updating occurs.
  - **Use case:** Updating the DOM whenever state or props change.
  - **Should I call setState?:** Yes.

#### Unmounting

Unmounting is when a component is removed from the DOM.

The following method can be called in relation to component unmounting.

- `componentWillUnmount`
  - invoked immediately before a component is unmounted and destroyed
  - **Use case:** Removing a component after being used.
  - **Should I call setState?:** No.


#### Other methods

- `setState`
  - This is the primary method used to update the user interface in response to event handlers and server responses. `setState` causes the component and its children to be re-rendered. Note that changing state using `setState` is asynchronous, so it does not always immediately update the component.
- `forceUpdate`
  - Will cause the component to re-render. Use if your `render` method depends on other data and you want to force this component to render. You should try to avoid using this method.

### Code Example


```jsx
import React from 'react';

class App extends React.Component {

   constructor(props) {
      super(props);

      this.state = {
         data: 0
      }

      this.setNewNumber = this.setNewNumber.bind(this)
   };

   setNewNumber() {
      this.setState({data: this.state.data + 1})
   }

   render() {
      return (
         <div className="row">
           <div className="col-md-4 offset-md-4">
              <Content myNumber = {this.state.data}></Content>
              <button className="btn btn-primary" onClick = {this.setNewNumber}>Click It! {this.state.data}</button>
            </div>
         </div>
      );
   }
}

class Content extends React.Component {

   componentWillMount() {
      console.log('Component WILL MOUNT!')
   }

   componentDidMount() {
      console.log('Component DID MOUNT!')
   }

   componentWillReceiveProps(newProps) {
      console.log('Component WILL RECIEVE PROPS!')
   }

   shouldComponentUpdate(newProps, newState) {
      return true;
   }

   componentWillUpdate(nextProps, nextState) {
      console.log('Component WILL UPDATE!');
   }

   componentDidUpdate(prevProps, prevState) {
      console.log('Component DID UPDATE!')
   }

   componentWillUnmount() {
      console.log('Component WILL UNMOUNT!')
   }

   render() {
      return (
         <div className = "card col-md-6">
           <div className="card-block">
              <h2 className="card-title">Lifecycle Hooks</h2>
              <h3 className="card-title">Check the console</h3>
              <p className="card-text">After five seconds the component will unmount</p>
            </div>
         </div>
      );
   }
}

export default App;
```


#### Live Example

![lifecycle-example.gif](https://tiy-learn-content.s3.amazonaws.com/de36df0f-lifecycle-example.gif)




### Conclusion

The component lifecycle allows us to exert control over the way React applies updates to the DOM. Data flows downward, from parent component to its children. The three main steps of the lifecycle process are mounting, updating, and unmounting. The virtual DOM is re-rendered any time there is an update, but only with the changed elements. We have touched on props and state here, but will delve deeper into the differences in the next lesson.

#### References/Resources

![react-and-flux-life-cycle-with-jsx-react-router-and-jest-unit-testing-4-638.jpg](https://tiy-learn-content.s3.amazonaws.com/d63df371-react-and-flux-life-cycle-with-jsx-react-router-and-jest-unit-testing-4-638.jpg)

[React Lifecycle](https://facebook.github.io/react/docs/react-component.html)

[React cheatsheet](https://reactcheatsheet.com/)

[React lifecycle cheatsheet](https://gist.github.com/monicao/243958d7498ed9fabe78)
