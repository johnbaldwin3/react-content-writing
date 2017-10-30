## React for SPAs

React is a JavaScript library that allows the view to change when data changes. Only the necessary number of components are updated and rendered when data changes. Components are encapsulated and only care about their own state. Multiple components can be composed into more complex UIs.

*What that does this mean?* If we are authoring a messaging app, we would want a message to be rendered every time a new message hits the database. Most of the UI components don't need to be refreshed every time a message is added. React makes sure only the component with new data is refreshed, leaving the rest of the components as they are.

### Terminology

- **React** React is not really a framework, but a library for creating user interfaces. Unlike frameworks that rely on the MVC pattern in order to separate the view from the code, React focuses primarily on the concerns of the view using *components*.

- **Component**: Components let you divide the UI into smaller, reusable elements. These components are used to display data as it changes over time.

- **Virtual DOM**: React represents every DOM object with a corresponding virtual DOM object. A virtual DOM object is a representation of a DOM object, like a lightweight copy.

### References

[Thinking in React](https://facebook.github.io/react/docs/thinking-in-react.html)
