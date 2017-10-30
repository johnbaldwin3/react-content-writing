## Binding Functions in React

It's important to remember that functions are special objects. Just as functions are passed around like objects, they can also be bound to the component and passed down as properties. When we made our form we wrote an event handler and bound it to the component.

### Explaining `this`

In Javascript `this` functions differently based on the scenario it's used in. In a constructor, you use the `new` keyword to create a new object. In this case, `this` always refers to the new object being constructed. We've also talked about the reasons to use strict mode, as otherwise `this` gets set to the global object `window`. When a function is defined as a property of an object, it's called a method. In those cases, you can use `this` to bind properties to their parent component. The confusion arises because unlike regular variables, the `this` keyword does not have a scope, meaning nested functions do not inherit the `this` value of their parent function automatically. When you invoke a method inside of another function or component, the `this` value for the method is set to the object it was invoked upon, not the object it was invoked inside of.

We've dealt with this previously when creating event handlers. We added a line of code in the constructor function to bind the `this` in the event handler to the `this` of the parent component.

Let's look at an example similar to the one you've seen before:

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

### More Than One Solution

The above code is the recommended way to bind functions to a component, however there are some other options that will work. Let's take a look at a few other solutions:

```jsx
<input type="text" onChange={this.handleTopping.bind(this)} value={this.state.topping}/>
```

Or we could use an arrow function:

```jsx
onChange={e => this.handleTopping(e)}
```

The issue with the solutions above is that you may run into performance issues since the function is reallocated on every render. This makes both solutions sub-optimal.

While the first solution is recommended in the React docs, there is a new technique surfacing that makes for cleaner code. This solution involves using class properties and the arrow function.

```jsx
handleTopping = (e) => {
  this.setState({topping: e.target.value})
}
```

By writing the code this way, we're taking a method and turning it into an expression. And by using the arrow function syntax we're gaining access to the `this` property of the component, saving us from needing to use the bind method. While this method is available in ES6 (ECMAScript 2015), it's experimental and may be removed in later iterations. **Please use with caution as it may be removed at a later date.**


### Conclusion

`this` is not always what we think it is. Especially when invoking a function inside a method. In order to make sure `this` is bound to the right context in React components, we explicitly bind it in the constructor method. There's more than one solution to this problem, but binding in the constructor method is the recommended solution.

#### References

- [Todd Motto](https://toddmotto.com/understanding-the-this-keyword-in-javascript/)
- [GitHub Gist](https://gist.github.com/amitai10/adb66d6faa714e8c3cdb94946bb98356)
