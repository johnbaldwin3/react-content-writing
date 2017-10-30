## Styling Components with React
React's foundation centers around modularizing (creating stand-alone pieces of code) code to keep everything self-contained. React JSX components allow us to write Javascript and HTML in a single file, and takes the same approach when it comes to styling. There are just a few new rules and concepts to abide by:

* It's common practice in React to create self-contained components.
* Styling can take place by using the `className` attribute and creating a stylesheet to transform our component.
* We can also style directly inline with React using a few approaches.
* Multiword style properties should obey the camelCase (`backgroundColor`) naming convention. Exceptions are the `data-` and `aria-` properties, which remain separated by a dash.

### Examples
In HTML, as in JSX, we have the ability to designate a class (HTML) or *classNames* (JSX).
Inside of the `render` method before the `return` statement we can assign styling to a variable and pass that variable to elements inside of the component. Adding a `style` attribute to the element allows us to pass a variable in as the value using `{}` brackets: `style={yourVariableHere}`. This method is a great choice when dealing with a lot of styles or a larger component.

```js
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

### References
* [Kirupa.com](https://www.kirupa.com/react/styling_in_react.htm)
* [React Docs](https://facebook.github.io/react/docs/dom-elements.html)
* [React JSX](https://facebook.github.io/react/docs/jsx-in-depth.html)

