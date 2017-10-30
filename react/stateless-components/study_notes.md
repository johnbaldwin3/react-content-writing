## Stateless Components
State isn't required in React components. In fact, you can have components that rely only on the props. If you're not changing any data in the component, then there's no need for state - simply use props to pass static data.

### Terminology
* **Stateless Component** — Only props, no state. There's not much going on besides the render() function whose logic revolves around the props they receive. This makes them very easy to follow and test.We sometimes call these **presentational components**.
* **Stateless Functional Component** - If your component only has a render method, you can write it as a stateless functional component, and your function will be passed `props` as its first argument
* **Stateful Component** — Both props and state. We also call these state managers. They are in charge of client-server communication, processing data, and responding to user events. We sometimes call these **container** components.

### Examples

#### Stateless Component
```jsx
class List extends Component {
  render() {
  return (
    <div>
      <h3>Favorite Movie List: </h3>
      <ul className="list-group">
        {this.props.movies.map((movie, index)=>{
          return (
            <li className="list-group-item" key={movie.title}>
            <h3>{movie.title}</h3>
            </li>
          )
        })}
      </ul>
    </div>
    );
  }
}
```

#### Stateless Functional Component
```jsx
const List = ({movies}) => {
  return (
    <div>
      <h3>Favorite Movie List: </h3>
      <ul className="list-group">
        {movies.map((movie, index)=>{
          return (
            <li className="list-group-item" key={movie.title}>
            <h3>{movie.title}</h3>
            </li>
          )
        })}
      </ul>
    </div>
    );
  }
}
```

#### Stateful Component
```jsx
export default class List extends Component {
  constructor(props){
    super(props);

    this.handleMovie = this.handleMovie.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);

    this.state = {
      movies: [],
      title: "",
    };
  }
  handleMovie(e){
    this.setState({title: e.target.value});

  }
  handleSubmit(e) {
    e.preventDefault();
    this.state.movies.push({movieTitle: this.state.title});
    this.setState({movie: this.state.movies, title: ""});

  }
  render() {
    return (
      <div className="movie-list">
        <h3>Favorite Movie List: </h3>
        <form onSubmit={this.handleSubmit}>
          <input type="text" onChange={this.handleMovie} value={this.state.title}/>
          <input type="submit" value="Add Movie" />
        </form>
        <MovieList movie={this.state.movies}/>
      </div>
    );
  }
}
```

### References
* [JSPlayground](http://javascriptplayground.com/blog/2017/03/functional-stateless-components-react/)
* [Todd Motto](https://toddmotto.com/stateful-stateless-components)
* [Dan Abramov](https://medium.com/@dan_abramov/react-components-elements-and-instances-90800811f8ca)
