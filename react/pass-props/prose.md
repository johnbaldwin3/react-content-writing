## Passing Data via Props to Child Components

Let's examine how data is passed around between components. We've already been doing this in previous examples, but now we're going to go more in depth on *how* these processes work.

Each component should be responsible for a minimal number of elements and minimal functionality. Data management and distribution throughout a project should be handled by multiple components. We should have a lot of "presentational" components that inherit their properties from "container" components. Each should be compartmentalized so that the code can be accessed and reused in the project multiple times if need be.

### The List App

The following example will demonstrate passing props between components and the functionality we gain by doing so.

Let's envision an application that writes a list, maybe an attendance-list-maker for a teacher.

Before we even look at the code, let's think about some of the parts the application would need:

* It needs a way to enter a student's name with a button to submit that name to a list of students.
* It needs some visual representation of the list. We'll use a simple unordered list for this example.
* When a student's name is entered, it will be pushed into an array of students, and then the array will be passed down to the component that renders the list on our web page.

#### The App Build

Let's start with the name input form.

```jsx
export default class App extends Component {
  constructor(props){
    super(props);

    this.handleName = this.handleName.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);

    this.state = {
      students: [],
      name: "",
    };
  }
  handleName(e){
    this.setState({name: e.target.value});

  }
  handleSubmit(e) {
    e.preventDefault();
    this.state.students.push({studentName: this.state.name});
    this.setState({students: this.state.students, name: ""});

  }
  render() {
    return (
      <div className="class-maker">
        <h3>Create Your Class List Here: </h3>
        <form onSubmit={this.handleSubmit}>
          <input type="text" onChange={this.handleName} value={this.state.name}/>
          <input type="submit" value="Add Student" />
        </form>
        <StudentList students={this.state.students}/>
      </div>
    );
  }
}
```

There's a lot going on, so let's break this into bite size chunks and tackle them one at a time.

Lets start with the `render()` method on our `<App />` component.

```jsx
render() {
  return (
    <div className="class-maker">
      <h3>Create Your Class List Here: </h3>
      <form onSubmit={this.handleSubmit}>
        <input type="text" onChange={this.handleName} value={this.state.name}/>
        <input type="submit" value="Add Student" />
      </form>
      <StudentList students={this.state.students}/>
    </div>
  );
 }
}
```
Let's note of a few details:

* We have a `<form>`that contains a text `<input />` and a `<input type="submit" />` that functions as our submit button.
* On our form we have a `onSubmit` property and have given it a value of `{this.handleSubmit}`. We'll go more into this later. For now, just take note that this is happening.
* On our `<input type="text" />` we have an `onChange=` property that has a value of `{this.handleName}` and we've given the input itself a value of `value={this.state.name}`.
* We need that value from the input, because that is how we will grab the name that the teacher types into the input.

Now let's look at the methods we called on our `<App />` component. We've already defined where these methods will be used, now let's define what they do.

```jsx
export default class App extends Component {
  constructor(props){
    super(props);

    this.handleName = this.handleName.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);

    this.state = {
      students: [],
      name: " ",
    };
  }
  handleName(e){
    this.setState({name: e.target.value});
  }
  handleSubmit(e) {
    e.preventDefault();
    this.state.students.push({studentName: this.state.name});
    this.setState({students: this.state.students, name: " "});
  }
}
```

Some takeaways from this portion of our `<App />` component:
* We have a `constructor(props)` with `super(props)` called inside of it. This should be familiar as all components created as a `class` should have a base constructor that receives props.
* We provide reference to `this` (the component) with each of the handler methods: `this.handleName = this.handleName.bind(this);` and `this.handleSubmit = this.handleSubmit.bind(this);`.

The initial state is being set within the constructor:

```jsx
this.state = {
  students: [],
  name: " ",
};
```

That lets the component know which properties change in order to keep track of them. In this case, we want it to track an empty array called `students` and a string called `name` that is initially empty.

Next, let's look at our methods `handleSubmit` and `handleName`.

```jsx
handleName(e){
  this.setState({name: e.target.value});
}
handleSubmit(e) {
  e.preventDefault();
  this.state.students.push({studentName: this.state.name});
  this.setState({students: this.state.students, name: " "});
}
```

* Inside of `handleName` we pass an argument `e` that is our `event` object. The `onChange` property listens for changes to the value of the `<input />` and fires each time a key stroke is registered.
* We then take the `e.target.value` which gives us the value correlated to our input and store it in the `state` of `name`; `this.setState({name: e.target.value});`.
* This updates our `state` which can be retrieved throughout our component at any time.
* `handleSubmit` is also provided with an `event` object using the shorthand `e`.
* This allows us to call the `e.preventDefault()` method which prevents the form from trying to POST to the server.
* Next, we grab the current `state` value of our `name` and `push` that value into our `students` array:

```jsx
this.state.students.push({studentName: this.state.name});
```

We pass the array an object with the property `studentName` and the value `this.state.name`. This ensures that each time we hit submit, a new name will be added to our array.

* After that, we update the `state` using `setState` to make sure our component is re-rendered.

```jsx
this.setState({students: this.state.students, name: ""});
```

* We also update the value of `state.name` back to an empty string. This clears our input box since its value is the value of `this.state.name`.

The `<App />` component is concerned with handling and updating the `state` of the student list. Now let's check out how we get that list to render on our application.

### Pass the Props

Inside of our `return` statement:

```jsx
return (
  <div className="class-maker">
    <h3>Create Your Class List Here: </h3>
    <form onSubmit={this.handleSubmit}>
      <input type="text" onChange={this.handleName} value={this.state.name}/>
      <input type="submit" value="Add Student" />
    </form>
    <StudentList students={this.state.students}/>
  </div>
);
```

We placed our `<StudentList />` component. This component was given a property `students` and passed the value of `this.state.students`. This gives access to the state properties to `<StudentList />` component in the form of `props`. Now let's peek inside of our `<StudentList />` component and see how it works:

```jsx
class StudentList extends Component {
  constructor(props){
    super(props);

  }
  render(){
    let kids = this.props.students.map((student, index) => {
      return (
        <li key={index}>{student.studentName}</li>
      )
    })
    return(
      <div>
        <h4>My Class:</h4>
        <ul>
          {kids}
        </ul>
      </div>
    );
  }
}
```

What to note:
* Make sure to pass the `constructor()` and `super()` with `props` to the component.
* Inside of our render method, we declare a variable using the ES2015 `let` syntax: `let kids =`.
* We set the value of that to :

```jsx
this.props.students.map((student, index) => {
  return (
    <li key={index}>{student.studentName}</li>
  )
})
```

* We `map` over `this.props.students` (which was passed down from the `<App />` components in the form of `this.state.students`).
* We extract each student from that array and return an index and student as a list item:
`<li key={index}>{student.studentName}</li>`.
* `student.studentName` references the `studentName` property of each `student` object in the `students` array.
* Each mapped item needs a unique `key`, so we use the `index` of each object being mapped over for simplicity sake. `key={index}`.
* We then insert the newly created array of list items (`kids`) using bracket notation with `{kids}`

And that's it! We have successfully taken data from a parent component and shared it down to a child component using `props`.

### Conclusion
* `props` allow for the transfer of data, while protecting the `state` and management of `state` in the parent component.
* We looked at setting the `state` (`this.setState({})`),  and how we can keep track of data within a component by using `state`.
* We looked briefly at binding `this` to the component's methods (`this.handleSubmit = this.handleSubmit.bind(this)`) which gave us access to `this` for the component.
* We examined how `e.target.value` (or `event.target.value`) can be used to get value from inputs. The input values can then be stored in the state for later use.
* We used the `event.preventDefault()` method to stop our form from trying to post to a server.

#### References
[React Docs](https://facebook.github.io/react/docs/state-and-lifecycle.html)
