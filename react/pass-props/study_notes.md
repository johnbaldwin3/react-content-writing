## Pass data via props to children React components

With React, each component should be responsible for a minimal number of elements and minimal functionality. Data management and distribution throughout a project should be handled by multiple components. We should have a lot of "presentational" components that inherit their properties from "container" components. Each should be compartmentalized so that the code can be accessed and reused in the project multiple times if need be.

### Examples

`<App />` is a "container" component which renders a "presentational" component within. It saves user input to its `state` and passes the data to `<StudentList />` via a `students` property.

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

### Setting State and Sharing Props
#### Setting Initial State

Here we assign the initial values of the app's state.

```jsx
export default class App extends Component {
  constructor(props){
    super(props);

    // Method binding. We will explain this in detail in the next lessons.
    this.handleName = this.handleName.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);

    // Set initial state:
    this.state = {
      students: [],
      name: "",
    };
  }
  // Handler and render methods...
}
```
* That simply lets the component know what changes it needs to keep track of. In this case, we want it to track an empty array called "students" and a variable called "name" that is initially set to an empty string.

#### Changing State

```jsx
// render() method in <App /> component.
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

* When one of these values changes in a component, the state has to be updated by using the `this.setState()` method.
* We have a `<form>`that contains a text `<input />` and a `<input type="submit" />` that functions as our submit button.
* On our form we have a `onSubmit` property and have given it a value of `{this.handleSubmit}`. We'll go more into this later. For now, just take note that this is happening.
* On our `<input type="text" />` we have an onChange= property that has a value of `{this.handleName}` and we've given the input itself a value of `value={this.state.name}`.
* We need that value from the input because that is how we will grab the name that the teacher types into the input.

#### Methods

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
  // Render method...
}
```

* We have a `constructor(props)` with `super(props)` called inside of it. This should be familiar as all components are created as a class should have a base constructor that receives props.
* We'll examine the two unfamiliar expressions `this.handleName = this.handleName.bind(this);` and `this.handleSubmit = this.handleSubmit.bind(this);` in the next lesson. For now, just understand that we are giving the two methods access to `this`.
* Inside of handleName we pass an argument e that is our event object. The onChange property listens for changes to the value of the <input /> and fires each time a key stroke is registered.
* We then take the `e.target.value` which gives us the value correlated to our input and store it in the state of "name" : like so, `this.setState({name: e.target.value});`.
* This simply updates our state which can be retrieved throughout our component at any time.
* `handleSubmit`, and see that we again pass it an event object using the shorthand e.
* This allows us to call the `e.preventDefault()` method which prevents the form from trying to POST to the server.
* Next, we grab the current (state) value of our name and push that value into our student's array:

```jsx
this.state.students.push({studentName: this.state.name});
```
* We pass the array an object with the property studentName and the value `this.state.name`. This ensures that each time we hit submit, a new name will be added to our array.

```jsx
this.setState({students: this.state.students, name: ""});
```
* We update the state using `setState` to make sure we have saved our changes.
* Update the value of our name state back to an empty string (this clears our input box, since it's value is the value of `this.state.name`).

### Passing Props to Child Components

#### Parent Component
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

* The `<StudentList/>` is given a property students and passed the value of `this.state.students`.
  * This gives access to the state properties to `<StudentList />` component in the form of `props`.

#### Child Component


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

* Make sure to pass the constructor() and super() with props to the component.

```jsx
this.props.students.map((student, index) => {
  return (
    <li key={index}>{student.studentName}</li>
  )
})
```

* Inside of that method we `map` over `this.props.students` (which was passed down from the `<App />` components in the form of this.state.students).
* We extract each student from that array and return an index and student as a list item : `<li key={index}>{student.studentName}</li>`.
* The `student.studentName` give us access to the `studentName` property inside of our students array.
* We know that each mapped item needs a unique key, so we use the index of each item being mapped over for simplicity sake. `key={index}`.
* We then insert each mapping using bracket notation with` {kids}`. That is put into the return statement where the `<ul> {kids} </ul>` is placed.
### References
[React Docs](https://facebook.github.io/react/docs/state-and-lifecycle.html
[Presentational and Container Components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)
