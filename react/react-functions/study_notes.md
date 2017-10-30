## Author functions in a React component and bind them to the component

In Javascript `this` functions differently based on the scenario it's used in. In a constructor, you use the `new` keyword to create a new object. In this case, `this` always refers to the new object being constructed. We've also talked about the reasons to use strict mode, as otherwise `this` gets set to the global object `window`. When a function is defined as a property of an object, it's called a method. In those cases, you can use `this` to bind properties to their parent component. The confusion arises because unlike regular variables, the `this` keyword does not have a scope, meaning nested functions do not inherit the `this` value of their parent function automatically. When you invoke a method inside of another function or component, the `this` value for the method is set to the object it was invoked upon, not the object it was invoked inside of.

### Examples

```jsx
export default class List extends Component {
  constructor(props){
    super(props);

    this.handleTopping = this.handleTopping.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);

    this.state = {
      pizza: [],
      topping: "",
    };
  }
  handleTopping(e){
    this.setState({topping: e.target.value});

  }
  handleSubmit(e) {
    e.preventDefault();
    this.state.pizza.push({pizzaTopping: this.state.name});
    this.setState({pizza: this.state.pizza, topping: ""});

  }
  render() {
    return (
      <div className="pizza-maker">
        <h3>Favorite Pizza Toppings List: </h3>
        <form onSubmit={this.handleSubmit}>
          <input type="text" onChange={this.handleTopping} value={this.state.topping}/>
          <input type="submit" value="Add Topping" />
        </form>
        <ToppingsList pizza={this.state.pizza}/>
      </div>
    );
  }
}
```

In the above example, we're allowing the user to input their favorite toppings for pizza. We created an event handler to handle the user input of toppings called `handleTopping`. We invoked that handler on `this` inside the `render` method using the `onChange` function. We want the `this` context to come from the top level component. This is important because we want that handler (method) to have access to the properties, state and methods of the component. To ensure `this` is bound to the correct context, we explicitly write a line of code in the constructor method to bind our event handler to the `this` of the component: `this.handleTopping = this.handleTopping.bind(this);`.

#### Other Options

Within an event listener

```jsx
<input type="text" onChange={this.handleTopping.bind(this)} value={this.state.topping}/>
```

Arrow function:

```jsx
onChange={e => this.handleTopping(e)}
```

Expression Arrow Function

```jsx
handleTopping = (e) => {
  this.setState({topping: e.target.value})
}
```

#### References

- [Todd Motto](https://toddmotto.com/understanding-the-this-keyword-in-javascript/)
- [GitHub Gist](https://gist.github.com/amitai10/adb66d6faa714e8c3cdb94946bb98356)
