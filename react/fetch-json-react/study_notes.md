## Fetching JSON
Using `fetch` to pull outside JSON data into our applications from an existing API.

* We can use the `fetch` method in React in order to make a network request.
* We use `then` to manage our promises and make sure our network request is completed.
* We can use `catch` to listen for error messages from the network.
* We can store our data in `state`, using `setState` inside of our promises.
* `componentDidMount` is the ideal method in which to make network requests.
* `state` can be passed down as `props` to children components.

### Examples

The `App` component ("container" component) performs the `fetch` and passes data down to `CharacterList` ("presentation" component) via `state`. `CharacterList` has access to the data via `this.props.people`.

```jsx
export default class App extends Component {
  constructor(props) {
    super(props);

    this.state = {
      characters: [],
    }
  }
  componentDidMount() {
    fetch('http://swapi.co/api/people/')
    .then(results => results.json())
    .then(responseData => {
      this.setState({characters: responseData.results});
    })
    .catch((error) => {
      console.log("Error with Fetching : ", error);
    });

  }
  render() {
    console.log("characters", this.state.characters);
    return (
      <div className="main">
        <CharacterList people={this.state.characters}/>
      </div>
    );
  }
}
```

```jsx
class CharacterList extends Component {
  constructor(props) {
    super(props);

  }
  render() {
    let peeps = this.props.people.map((person, index) => {
      return (
        <li key={index} className="personList">
          <div className="persona">
            <h4 className="name">{person.name}</h4>
            <h5 className="gender">Gender: {person.gender}</h5>
            <h5 className="eyes">Eye Color: {person.eye_color}</h5>
            <h5>Hair Color: {person.hair_color}</h5>
            <h5>Height: {parseInt(person.height) / 100} meters</h5>
            <h5>Mass: {person.mass} kilograms</h5>
            <h5>Appears in {person.films.length} films.</h5>
          </div>
        </li>
      )
    })
    return (
      <div className="characters">
        <ul className="character-ul">
          {peeps}
        </ul>
      </div>
    )
  }
}
```

### References
* [MDN Then Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
* [MDN Body.json()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)
* [MDN Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
* [StarWars API : SWAPI](https://swapi.co/)
* [React Component Lifecycles](https://facebook.github.io/react/docs/react-component.html#componentwillreceiveprops)


