## Styling Components with React
We've already covered the building of components and data flow in `state` and `props`, but our websites have been pretty underwhelming so far. We haven't concentrated much on the styling aspects available to us when building React applications. The ability to apply a style based on a class or using inline styles in HTML has long been a tool for software engineers. React allows us to do the same sort of styling inside of our components within our JSX elements. The functionality is not much different, though some of the properties and declarations need to be a bit different to function in our JSX.

React's foundation centers around modularizing (creating stand alone pieces of code) our code to keep everything self-contained. React JSX components allow us to write our Javascript and HTML in a single file. React takes the same approach when it comes to styling. Let's take a look at how React suggests we style our components.

### Using `classNames`
In HTML, as in JSX, we have the ability to designate a class (HTML) or *classNames* (JSX). Let's see the HTML approach first and then we'll examine the same situation within React.

Below is some boilerplate HTML with a few classes:

```html
<body>
  <nav>
    <header class="header">Header</header>
  </nav>
  <div class="box">
    <h3 class="title">An Interesting Title</h3>
  </div>
  <div class="box">
    <h3 class="title">An Interesting Title</h3>
  </div>
  <div class="box">
    <h3 class="title">An Interesting Title</h3>
  </div>
</body>
```

Given this HTML we could easily style our elements using CSS. In our CSS stylesheet we'd write something similar to the following:

```css
.header {
  color: red;
}
.box {
  background-color: blue;
}
.title {
  color: white;
}
```

We created classes to target within our stylesheet and altered them according to our design. Now, let's visit how we would approach the same problem with React:

```jsx
class App extends Component {
  constructor(){
    super();
  }
  render(){
    return (
      <body>
        <nav>
          <header className="header">Header</header>
        </nav>
        <div className="box">
          <h3 className="title">An Interesting Title</h3>
        </div>
        <div className="box">
          <h3 className="title">An Interesting Title</h3>
        </div>
        <div className="box">
          <h3 className="title">An Interesting Title</h3>
        </div>
      </body>
    )
  }
}
```

With React, our CSS stylesheet would be **exactly** the same as before. We'll target the same classes as the previous example to apply our styling.

```css
.header {
  color: red;
}
.box {
  background-color: blue;
}
.title {
  color: white;
}
```

Now, let's include our styles in our JSX component instead of an external stylesheet.

### Inline Styling
Similar to using inline styles in HTML, we can use inline styles in JSX components as well. There are just a few new rules and concepts to abide by:

* Multi-word CSS properties (commonly separated by a dash) such as `text-align`, `font-family`, or `background-color` must now adhere to JavaScript standards. They should be written in *camelCase* (all one word, with the first word lowercased and the second word capitalized). Previous examples would become: `textAlign`, `fontFamily`, and `backgroundColor`.
* Single worded CSS properties such as `border`, `color`, and `width`, will remain **unchanged** and used as they would be in CSS.

**Let's take a look at a couple of ways we can apply these inline styles in React.**

#### Using Variables

Inside of our `render` method before our `return` statement we can assign our styling to a variable and pass that variable to our elements. We can then add a `style` attribute to the element or component in question and pass our variable in as the value using `{}` brackets: `style={yourVariableHere}`. This method is a great choice when dealing with a lot of styles or a larger component.

```jsx
class App extends Component {
  constructor(){
    super();
  }
  render(){
    let headerStyle = {
      color: "red",
    };
    let boxStyle = {
      backgroundColor: "blue",
    };
    return (
      <body>
        <nav>
          <header className="header" style={headerStyle}>Header</header>
        </nav>
        <div className="box" style={boxStyle}>
          <h3 className="title">An Interesting Title</h3>
        </div>
        <div className="box" style={boxStyle}>
          <h3 className="title">An Interesting Title</h3>
        </div>
        <div className="box" style={boxStyle}>
          <h3 className="title">An Interesting Title</h3>
        </div>
      </body>
    )
  }
}
```

`<div className="box">` is styled to have a blue background. What if we wanted to control the color for each instance of this div? We could first create a property `bgroundCol` on each `<div className="box">`. Then apply the value of each `bgroundCol` property as the `backgroundColor` for the `boxStyle` to be applied to that element. We'll use `this.props.bgroundCol` to access the value of each element's `bgroundCol` property.

```jsx
let headerStyle = {
  color: "red",
};
let boxStyle = {
  backgroundColor: this.props.bgroundCol,
};
return (
<nav>
  <header className="header" style={headerStyle}>Header</header>
</nav>
<div className="box" bgroundCol="blue" style={boxStyle}>
  <h3 className="title">An Interesting Title</h3>
</div>
<div className="box" bgroundCol="green" style={boxStyle}>
  <h3 className="title">An Interesting Title</h3>
</div>
<div className="box" bgroundCol="brown" style={boxStyle}>
  <h3 className="title">An Interesting Title</h3>
</div>
  )
}
```

By passing our `backgroundColor:` property the value of `this.props.bgroundCol`, we are able to style directly inline as we see fit.

#### Completely Inline

We can take this one step further by styling everything completely inline. Let's take a look at how this would work by creating a new div and giving it a `style` attribute. We can then pass in our properties as an object, like so:

```jsx
<div className="new" style={{color:"orange", backgroundColor: "purple", fontSize: "33px", textAlign:"right", height: 80}} >Im the best Div ever </div>
```
**Note that double brackets : we are passing our first set of brackets an object containing our styling**

[callout-info]
The majority of the properties that involve a default value of pixels (px) can either exist as a string, `"33px"` or `"33"`, or a straight number such as `80`. The compiler knows to add 'px' on the end when it renders. (There are a few exceptions that you may find).
[/callout-info]

Hopefully, this provided a comprehensive overview of how to style your React components.

### Conclusion
* It's common practice in React to create self-contained components.
* Styling can take place by using the `className` attribute and creating a stylesheet to transform our component.
* We can also style directly inline with React using a few approaches.
* Multiword style properties should obey the camelCase (`backgroundColor`) naming convention. Exceptions are the `data-` and `aria-` properties, which remain separated by a dash.

#### References
* [Kirupa.com](https://www.kirupa.com/react/styling_in_react.htm)
* [React Docs](https://facebook.github.io/react/docs/dom-elements.html)
* [React JSX](https://facebook.github.io/react/docs/jsx-in-depth.html)
