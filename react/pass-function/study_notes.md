## Passing a Function Via Props

* Passing a function via `props` works exactly the same way the passing any other data via `props` would work.
* The child component can actually call and fire the function on the parent component.
* Using this method allows `state` to reside in the parent component and not be spread into more components than necessary.

### Examples

Parent component ("container" component)

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
        <h1>Color Me Badd</h1>
        <ColorMaker changeColor={this.changeColor} />
      </div>
    );
  }
}
```

Child component ("presentational" component)

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

Within `<ColorMaker />`, `this.props.changeColor` refers to the `changeColor` method in the `<App />` component.

### References

* [React Docs](https://facebook.github.io/react/docs/state-and-lifecycle.html)
