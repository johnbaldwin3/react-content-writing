## Implementing a Form on a React Component

By now you should have a grasp on some basic fundamentals of React. How do we begin to add functionality to our app? We want to be able to capture the user's input and have the app react accordingly. Forms are a great tool to do this. Forms in React are a little different, in that the HTML form elements already hold some internal state. Let's start by making a simple form to collect the user's name. We'll go through the process of creating the form step by step, and then put it all together at the end.

### Collecting Input

To collect input from the user you'll first you need to create a Form component. Since we expect the data to change, we will use *state* to manage the input (rather than *props*). When we first create the component we can initialize the state of the component. You'll remember from previous lessons and exercises that we create a React component by extending it on a `class`. We then use the `constructor` method to initialize the state and include the `super` function to ensure that the value of `this` points to the parent constructor class.

```jsx
class Form extends React.Component {
  constructor(props){
    super(props)
  }
}
```

Components must always have a `render` function. This tells React what to display in the DOM. The `render` function should return a single React element. We could write it like this:

```html
render(){
  return (
    <form>
      <input name="name" type="text" value="name" />
    </form>
  )
}
```

However, this would mean that the *value* is always set to `"name"` and cannot be changed by the user. To allow the user to change the value, we can make it dynamic by allowing it to be updated from the state:

```html
render(){
  return (
    <form>
      <input name="name" type="text" value={this.state.name} />
    </form>
  )
}
```

In order for React to know when a user changes the value of the state for that element, we need to add an event handler to capture the change:

```jsx
handleNameChange(event){
  this.setState({name: event.target.value})
}
```

The event handler is placed in the code above the `render` method. The event in this case is the user typing into the input form. The event is then passed into the handler and targets the value changed in the event by using the `setState` method to update the state with the changed value.

You can name event handlers whatever you'd like, but general best practice is to use the word 'handle' along with the change that it's dealing with. Ours is `handleNameChange`.

But wait, how is the `handleNameChange` function called? We need to use the `onChange` event listener to call the `handleNameChange` function when a `change` event is fired from our input field. The `handleNameChange` function will capture the change in input.

```jsx
render(){
  return (
    <form>
      <label>
        Your Name:
        <input name="name" type="text" value={this.state.name} onChange={this.handleNameChange}/>
      </label>
    </form>
  )
}
```

Now that we've added the `handleNameChange` function, we need to bind it to the scope of the component. If we forget to bind `this` to the handler being called on the component, it will cause an error as `this` will be `undefined`.

```jsx
this.handleNameChange = this.handleNameChange.bind(this);
```

The above code needs to be written inside the constructor method of the component. Since the constructor method is where we set the initial state, we can set the state of the `name` input to an empty string, as we are expecting the input to be text. Let's put those both into the constructor:

```jsx
class Form extends React.Component {
  constructor(props){
    super(props)

    this.handleNameChange = this.handleNameChange.bind(this);
    this.state = {name: ''};
  }
}
```

Our form is coming along nicely, but we're missing one thing. Since this is a form, a user should expect to submit upon hitting enter. Let's create an event handler to handle the form submission and show the user an alert when it happens:

```jsx
handleSubmit(event){
  event.preventDefault();
  alert('Thank you, ' + this.state.name + ' your name was submitted');
}
```

Note that we used the special `event.preventDefault()` method here. Most people's natural tendency is to hit the enter button after typing in some text. Most of the time you will have more than one input field in a form, and the default behavior when hitting the enter key is that the form is submitted. You would not want this to happen if there are fields the user still needs to fill out before submitting. It's best to get in the habit of placing this function in your `handleSubmit` to avoid submitting the form early.

Now that we have the `handleSubmit` method we need to add an event listener to our form. Using the React `onSubmit` event listener, we will call the `handleSubmit` method when the form is submitted via `<input type="submit" value="Submit" />`.

The last bit we need to add is the same thing we did with our other event handler. We need to bind `handleSubmit` to `this` in the constructor. We also need to add the submit button. Then our React component will be ready for the red carpet.

Here is the final version of the component in it's entirety:

```jsx
class Form extends React.Component {
  constructor(props){
    super(props);

    this.handleNameChange = this.handleNameChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);

    this.state = {name: ''};
  }
  handleNameChange(event){
    this.setState({name: event.target.value});
  }
  handleSubmit(event){
      event.preventDefault();
      alert('Thank you, ' + this.state.name + ' your name was submitted');
  }
  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Your Name:
          <input onChange={this.handleNameChange} name="name" type="text" value={this.state.name}/>
        </label>
        <input type="submit" value="Submit" />
      </form>
    )
  }
}
```

### Conclusion

When making a form in React, you can connect the input changes to the state. Initialize the state in the constructor method. Target any changes, as well as the submittal of the form, with an event handler. Use the `setState()` method to update the state and re-render. Make sure to bind the event handlers to `this` in the constructor method. Don't forget to use the `preventDefault()` function to avoid early submittal of the form.

#### References

- [Site point](https://www.sitepoint.com/work-with-forms-in-react/)
- [React Forms](https://facebook.github.io/react/docs/forms.html)
