### React DOM

React creates a **virtual DOM** by abstracting the **application DOM** and maintaining it in memory. 

The Virtual DOM is used to handle in-page interactions and updates from the server.

This is accomplished by comparing the *new state* with the *previous state*.

### Component Lifecycle Methods

#### Mounting

When the component is created (initialized) and then inserted into the DOM.

- `constructor`: called before the component is mounted
- `componentWillMount`: invoked immediately before mounting occurs (before render).  
- `render`: required and must contain a single element
- `componentDidMount`: invoked immediately after a component is mounted.

#### Updating

A component is re-rendered because a props or state change occurs.

- `componentWillReceiveProps`: invoked before a mounted component receives new props.
- `shouldComponentUpdate`: invoked before rendering, when new props or state are being received.
- `componentWillUpdate`: invoked immediately before rendering when new props or state are being received
- `componentDidUpdate`: invoked immediately after updating occurs

#### Unmounting

Component is removed from the DOM.

- `componentWillUnmount`: invoked immediately before a component is unmounted and destroyed

#### Other methods

- `setState`: primary method used to update the user interface in response to event handlers and server responses.
- `forceUpdate`: will cause the component to re-render