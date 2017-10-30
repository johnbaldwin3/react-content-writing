## Pass the Function

We've looked at passing `props` from a parent component down to its children components, but we haven't explored all of the different things that can be passed down as `props`. Not only can we pass data along from `state`, but we can also pass along functions. We can even pass along functions that are executed on the parent component, but fired from the child component.

### A Colorful Example

React works by constantly checking the `state` against changes in the DOM. Let's create an app that changes the color of the background when we click a button. We do so by passing down a function via `props` and firing from the child component but executing it on the parent component.

The first step is the parent component:

```jsx
//An array of colors for us to randomly sort through and apply to the background color
let colors = ["blue", "green", "red", "yellow", "orange", "purple", "pink", "tomato"];

export default class App extends Component {
  constructor(props){
    super(props);
    this.state = {
      color: ""
    }
    this.changeColor = this.changeColor.bind(this);
  }
  changeColor() {
    let num = Math.floor(Math.random()* colors.length);
    this.setState({color: colors[num]});
  }
  render(){
    return (
      <div className="main" style={{backgroundColor: this.state.color ? this.state.color : "red"}}>
        <h1>Color The Wind</h1>
        <ColorMaker changeColor={this.changeColor} />
      </div>
    );
  }
}
```

First we create an array, `colors`, that we could randomly pull from and apply that color to the background color of the desired `<div>`.

Next, we applied our base `constructor` with `super`, and both received `props`.

We then created a method `changeColor`:

```jsx
changeColor() {
  let num = Math.floor(Math.random()* colors.length);
  this.setState({color: colors[num]});
}
```

What we're doing is creating a variable `num` which will be a number between `0` and the length of our `colors` array. This means if we add colors or remove colors we will still be randomly picking from the entire array.

Inside of our `render` method we provided minimal elements to return, including the `<ColorMaker />` component.

In the  `<ColorMaker />` component we pass a `changeColor` property with a value of `this.changeColor` (referencing our `changeColor` method in the `<App />` component).

```jsx
<ColorMaker changeColor={this.changeColor} />
```

With those simple steps we are set up to pass the functions down to `<ColorMaker />`

#### Children With Prop Functions

As we saw above, we were able to pass a function as a property attribute to a child component. Let's now take a look at the way we handle that function inside the child component.

```jsx
class ColorMaker extends Component {
  constructor(props) {
    super(props);
  }
  render() {
    return (
      <div className="color-change-div">
        <button onClick={this.props.changeColor}>Change Color</button>
      </div>
    )
  }
}
```

Inside of our `<ColorMaker />` component, we see `constructor` and `super`.

On our `<button>` we give it an `onClick` attribute and set its value to `{this.props.changeColor}`. The `props.changeColor` method that we are referring to is the `changeColor` method from the parent component.

[Here it is in action.](http://screencast-o-matic.com/watch/cbhZIsXkxP)

### Conclusion

* Passing a function via `props` works exactly the same way the passing any other data via `props` would work.
* The child component can actually call and fire the function on the parent component.
* Using this method allows state to reside in the parent component and not be spread into more components than necessary.

#### References

* [React Docs](https://facebook.github.io/react/docs/state-and-lifecycle.html)
