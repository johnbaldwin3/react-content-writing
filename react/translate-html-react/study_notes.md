### Components

A component is a chunk of code that is responsible for rendering a specific portion of the UI (user interface). 

They function a lot like, well, JavaScript functions. They can accept inputs (called "props") and return elements describing what should appear on the screen.

## Nesting Components

Components can be nested to increase the organization of our application.

They can even be imported from other files:

```jsx
//############### mainbody.js ###############
import React, { Component } from 'react';

//importing Components
import TopPara from './toppara.js'
import BottomPara from './bottompara.js'

export default class MainBody extends Component {
  render() {
    return (
      <div className="main-body">
        <TopPara /> // Nested Component
        <BottomPara /> // Nested Component
      </div>
    );
  }
}
```
