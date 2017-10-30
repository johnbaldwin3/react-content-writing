## Iteration in React

A huge part of React stems from the way that it handles data and re-renders the page according to that data. 

React components can have components that render data and elements after iterating over that data.

Let's look at that simple application again. This application takes in an array of objects, and renders each object into it's own `<div>` on our website.


```jsx
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

let famousAstroPhysicists = [
  {
    id: 1,
    firstName: "Carl",
    lastName: "Sagan",
    alive: "false",
    nationality: "United States",

  },
  {
    id: 2,
    firstName: "Neil",
    lastName: "deGrasse Tyson",
    alive: "true",
    nationality: "United States",
  },
  {
    id: 3,
    firstName: "Stephen",
    lastName: "Hawking",
    alive: "true",
    nationality: "United Kingdom, England",
  },

];


export default class App extends Component {
  render() {
    let famedPhysicists = famousAstroPhysicists.map((physicist) => {
      return (
        <div key={physicist.id} >
          <h1>{physicist.lastName + ", " + physicist.firstName}</h1>
          <h2>Still alive: {physicist.alive}</h2>
          <h3>Nationality: {physicist.nationality}</h3>
        </div>
      )
    });
    return (
      <div className="App">
        {famedPhysicists}
      </div>
    );
  }
}
```

![science.png](https://tiy-learn-content.s3.amazonaws.com/fccd5132-science.png)
