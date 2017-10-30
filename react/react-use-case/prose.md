## Using React to Create a Single Page Application

### What Is React?

*React* is not really a framework, but a library for creating user interfaces. Unlike frameworks that rely on the MVC pattern in order to separate the view from the code, React focuses primarily on the concerns of the view using *components*. Components let you divide the UI into smaller, reusable elements. These components are used to display data as it changes over time.

### Why Use React?

React is a JavaScript library that allows the view to change when data changes. Only the necessary number of components are updated and rendered when data changes. Components are encapsulated and only care about their own state. Multiple components can be composed into more complex UIs.

*What that does this mean?* If we are authoring a messaging app, we would want a message to be rendered every time a new message hits the database. Most of the UI components don't need to be refreshed every time a message is added. React makes sure only the component with new data is refreshed, leaving the rest of the components as they are.

#### Components & Reusability

Think of a React app as a larger component made up of smaller 'container' components. These components hold the logic needed to process data. Each 'container' component is made up of even smaller 'simple' components. These 'simple' components are presentational components, responsible for rendering the 'container' components' data. Each component is responsible for *one thing*, only. This is known as the [Single Responsibility Principle.](https://en.wikipedia.org/wiki/Single_responsibility_principle). Using small components creates a separation of concerns and maximizes code reuse. This also generates modular testable code.

##### Component Basic Architecture and Hierarchy

In the example below, each box represents a component:

* FilterableProductTable (orange): contains the entirety of the example.
* SearchBar (blue): receives all user input.
* ProductTable (green): displays and filters the data collection based on user input.
* ProductCategoryRow (teal): displays a heading for each category.
* ProductRow (red): displays a row for each product.

![react_components.jpeg](https://tiy-learn-content.s3.amazonaws.com/b5d0f3bc-react_components.jpeg)

[callout-info]
Read more about component architecture and hierarchy on [Thinking in React](https://facebook.github.io/react/docs/thinking-in-react.html)
[/callout-info]

#### High-Performance Virtual DOM

When it comes to dynamically updating the DOM with JavaScript, React is very powerful. Updating the DOM is normally the Achilles' heel of web performance. Updating the DOM can create bottlenecks which negatively affect web performance and user experience. React does not update the actual DOM in its entirety with every view update. It maintains a *virtual DOM* where only the parts of a component in which the data has changed are updated in the view.

React does this by keeping the DOM in memory. After a view update is reflected in the virtual DOM, React compares the previous state of the component with the current state of the virtual DOM and decides how to apply these changes using the minimum amount of updates. These updates are then applied to the DOM, maximizing read/write performance.

#### Routing & Back-end

React does need help with two things; loading data from the back-end, and client-side routing. As a developer, you will need to incorporate other libraries, such as *Flux* to have a fully functional and robust app.

[callout-info]
It's worth mentioning that React has other internal processes that make it all work. You will soon learn about JSX, rendering a component's life cycle, props, and state.
[/callout-info]


### Use Case Scenarios

#### When to Use React

We've alluded to this already, but you should consider building an SPA with React when the view has to dynamically and automatically update based on frequent data changes. You also want to use React to create a high-performance SPA that can consume large amounts of data in a fluid, responsive, and seamless manner.

#### When Not to Use React

React is not ideal for projects where data change is minimal or when building a static site where the view is not manipulated by data.

### Conclusion

React is a powerful view library that makes it possible to build high-performance SPAs. React lends itself to scenarios where data changes frequently. It's component-based nature also makes the code highly reusable and testable.

#### References
[Presentational and Container Components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)
