## React Router and Single Page Applications
We've discussed single page applications before, (sometimes referred to as SPAs), and the benefit they present to making web applications. They give us the ability to quickly load and retain data without the need to refresh, making for a much simpler user experience. React Router is a tool that will help with design and implementation of SPAs.

##React Router. 
Think of a router as an air traffic controller. The air traffic controller makes sure that all of the planes know when to take off and land. Similarly, a router helps organize the routes a web application should follow, and directs the user or data inputs to the appropriate portions of our web application.

Air traffic controllers also make sure things run efficiently at the airport and try to maximize the flow of traffic so things keep moving––our router does the same thing. A router is designed to intercept information that would normally go to the server, decide what to do with it, and (in the case of React) determine which components should be rendered. That ability to stop communication from going all the way to the server really speeds up our applications and lets us work much more efficiently.

Now let's look at the React Router, and how to integrate it into our applications.

### Installing React Router
Assuming we have already set up a `create-react-app` application, or used a webpack with the necessary goods for a React application, we'll start there with an empty application.

First thing we will need to do is go into our terminal and `cd` into our project directory. For this mock up, lets pretend we are in `/TIY/code/router-project/`.

We are going to use npm to install React Router with the following code (again, in our project directory):

```
npm install --save react-router-dom
```

This will install all of the React Router dependencies for a *web application* that we need to get going inside of our project. This lesson is based off of the current version of React Router, **version^4.1.1**.

### Thinking About Our Application...
There are a couple of ways we can utilize React Router in our SPA, but here are the most important details:
1. Whether we are using a component or our index.js, React Router is the single source of output for our application.
  * That means that all of our application will flow through our routing components in order for React Router to work.
1. React Router will require the use of a few different key components working together.
  * We will examine the `<BrowserRouter>`, `<Route>`, `<Switch>`, and the `<Link>` components employed by React Router v4.

Since this is a simple application, we'll begin in our `index.js`. Normally we'd have a `ReactDOM.render()` statement that plugs our app into the container `<div>` in our HTML.

#### index.js
Inside of our *index.js* file, let's look at the set up for our app and how we incorporate the beginnings of our React Router app.

First we'll see our normal list of React dependencies (React and ReactDOM) being imported, as well as our style sheet. Underneath our styles import, we see the importing of React Router with the `{BrowserRouter, Route, Switch}` dependencies specifically.

```jsx
//######### index.js #############

//import React
import React from 'react';
import ReactDOM from 'react-dom';

//import Styles
import './styles/index.css';

//import React Router
import {BrowserRouter, Route, Switch} from 'react-router-dom';

//import Components
import App from './scripts/components/App';
import PageOne from './scripts/components/page_one';
import PageTwo from './scripts/components/page_two';

ReactDOM.render(
  <BrowserRouter>
    <Switch>
      <Route path="/page_one" component={PageOne} />
      <Route path="/page_two" component={PageTwo} />
      <Route path="/" component={App}/>
    </Switch>
  </BrowserRouter>

  ,
  document.getElementById('root'));
registerServiceWorker();
```

Looking at the code above, we can see that inside of our `ReactDOM.render()` statement we have a component wrapping our entire application called `<BrowserRouter>`. The `<BrowserRouter>` is a router that uses the HTML5 history API to keep the UI of your application in sync with the URL the user is on. The `<BrowserRouter>` allows us to return a single container for our application as is required in JSX.

The next component we see inside of `<BrowserRouter>` is the `<Switch>` component. `<Switch>` allows us to render a `<Route>` (which we will discuss shortly) based on a specific set of criteria, i.e. an exact URL match.

The `<Route>` component specifies the URL route that should exist for a given component. It has two major attributes; the `path=` and `component=`. The `path` attribute takes the name of the route that should exist for a given component, for example, `path='/page_one'`. Because `Switch` will match the route to the first criteria, the `Route` components should be listed in order of specificity––with the most complex routes listed first and the least complex listed last.

#### The Order of Routes
Let's pretend that we had written the first route component with a `path='/'`.

```jsx
<Route path="/" component={App}/>
<Route path="/page_one" component={PageOne} />
<Route path="/page_two" component={PageTwo} />

```

`Switch` would then look at our application, and since every route begins with a forward slash `/` they would all match the first route component. Therefore, no other route would rendered no matter what the URL was. Since we list the `path="/"` `<Route>` last, allows each component to be read and matched before finding a component that is just a slash.

We could make one change to this by using the `exact` path keyword. In the above example, where our routes are ordered from least complex to most, we could add `<Route exact path="/" component={App}/>` to our first route and therefore only if the path was a `/` would it be matched. However, there are problems with this logic when dealing with complex routes that are dynamic in nature (changing with data or input). The dynamic routes might fail to yield the expected results when using `exact`, so it's best practice to order our routes from most to least complex, to avoid issues.

```jsx
<Route path="/page_one" component={PageOne} />
<Route path="/page_two" component={PageTwo} />
<Route path="/" component={App}/>
```

#### The Component to be Rendered
As you can see from our very first code snippet, we also imported the components from our other files in our list of import statements.

These import statements allow us to utilize that component inside of our router (just as we could render them normally before a router). The second part of the route component is the  `component={}` attribute. Passing in the name of the component (as we imported it to be) tells the router to render the component when the correct path is met as a URL. So when we have the URL "`example.com/page_one`" we expect our path to math the first `<Route>` component and display the `<PageOne>` component to the user.

### A Look Inside of the Component
Now lets check out our `page_one.js` file (in our mock app) where our `<PageOne>` component is being exported from.

At the top of the page you'll see our normal imports of React and React component.

Then next major part of React router is seen in the following import state `import { Link } from 'react-router-dom';`.

The `<Link>` component is exactly what is sounds like, a link. This takes the place of our normal anchor tags `<a>` (but actually renders an anchor tag in HTML) and comes with some extra features.

```jsx
//######### page_one.js #############

import React, { Component } from 'react';
import { Link } from 'react-router-dom';

export default class PageOne extends Component {
  render() {
    return (
      <div className="App one"><div className="header">Page One!</div>
        <p className="para">Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
        <div><button className="btn"><Link to="/">Main Page</Link></button></div>
        <div><button className="btn"><Link to="/page_two">Page Two</Link></button></div>
      </div>
    );
  }
}
```

For UI purposes the `<Link>` component is wrapped inside of a button element. The real take away here is what goes on with `<Link>`.

```jsx
<Link to="/page_two">Page Two</Link>
```

The `<Link>` component has one primary attribute: `to=`. It simply specifies the route to which that link should take the user via React router. Here on our `PageOne` component we have links to our `MainPage` component and our `PageTwo` component inside of the two `<Link>` components. We can use any method we have already learned to provide text for the links between the opening and closing `<Link>` tags - we kept it simple here with plain text, but could have added some JavaScript by using `{}`.

It's important to know that what is actually rendered by the `<Link>` component is an anchor tag `<a>` for styling purposes, though we could pass a `className` to each link as well. In this instance, we could have styled the anchor tags by doing the following:

```css
/*******STYLE SHEET********/
.btn a {
  text-decoration: none;
  font-size: 20px;
  color: black;
}
```

Here we have a `className="btn"` for each of our `<button>` elements. Inside of those we have the anchor tag which we style via regular CSS in the above code snippet (we could also nest this using Sass).

### The End Result
Here's a simple three page application (with minimal styling for demonstration) built with React router:

![routing.gif](https://tiy-learn-content.s3.amazonaws.com/74aaffad-routing.gif)

### Conclusion
* React router allows us to create simple and efficient single page applications.
* We can use npm to install React router for web applications by typing: `npm install --save 'react-router-dom'` in our project folder in terminal.
* The `<BrowserRouter>` component allows us to use the history API for the browser, which in later projects we will examine the importance of.
* The `<Switch>` component allows us to match a `path=` to a `component=` and render that component only when the path matches the exact router specified.
* We organize our `<Route>` components by complexity of their `path=""` attribute. The more complex routes are listed at the top, and the least complex are listed at the bottom.
* Each `<Route>` component has two main attributes - the `path` and `component`. The path attribute is the URL endpoint we which to match against for our component to render. The component attribute is the component we wish to render when the paths match.
* Inside of our application components, we can import the `<Link>` component which will create an anchor tag element when rendered. `<Link>` takes a `to=""` attribute and specifies the path to which the user should be taken to upon some sort of event (click, etc.).

#### References
* [React Router](https://reacttraining.com/react-router/web/guides/quick-start)
