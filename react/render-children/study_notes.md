## Rendering Children Components in React

### Examples

`{this.props.children}` is used to pass components *or elements* into a parent component component. A parent component doesn't have any inherent awareness of nested components.

`{this.props.children}` allows for a component to render things passed into it, and doesn't require that the component even reside inside of the same script sheet.

```jsx
// baselayout.js

import React, {Component} from 'react';

export default class BaseLayout extends Component {
  constructor(props) {
    super(props);
  }
  render(){
    return (
      <div className="base">
        <nav className="navbar">
          <h3>Navigation Bar: A cocktail lounge for coders</h3>
        </nav>

        {this.props.children}

        <footer>
          <h3>This is the BaseLayout footer</h3>
        </footer>
      </div>
    );
  }
}
```

Now, we'll use the `<BaseLayout></BaseLayout>` component inside our `App` component. `<BaseLayout></BaseLayout>` will contain its own nested elements.

```jsx
// App.js

import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

//import components
import BaseLayout from './Components/baselayout';

export default class App extends Component {
  constructor(props){
    super(props);
  }
  render() {
    return (
      <BaseLayout>
        <div className="main">
          <h4>This is the body!</h4>
        </div>
      </BaseLayout>
    )
  }
}
```

### References
[React Components](https://facebook.github.io/react/docs/composition-vs-inheritance.html)
