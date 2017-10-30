## Stateless Components

State isn't required in React components. In fact, you can have components that rely only on the props. If you're not changing any data in the component, then there's no need for state - simply use props to pass static data.

### Component Types

There are three different component types: *stateless*, *stateless Functional*, and *stateful*.

**Stateless Component** — Only props, no state. There's not much going on besides the render() function whose logic revolves around the props they receive. This makes them very easy to follow and test.We sometimes call these **presentational** components.

Stateless components are pure functions of their props. They don't have lifecycle methods and don't retain internal state. Another way to think about **stateless** components is that they deal with the UI rather than behavior. This is why you'll also see them called **presentational** components.

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

**Stateless Functional Component** - If your component only has a render method, you can write it as a stateless functional component, and your function will be passed `props` as its first argument like so:

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

Another thing to note with the **stateless functional component** above is that there's no `this`, and there's no binding required.

**Stateful Component** — Both props and state. We also call these state managers. They are in charge of client-server communication, processing data, and responding to user events. We sometimes call these **container** components. These sort of logistics should be encapsulated in a moderate number of stateful components, while all visualization and formatting logic should move downstream into as many stateless components as possible.

You've seen (and written by now) stateful components. Imagine if you wanted to let the user interact by inputting their favorite movies. Here's an example to compare to the stateless components we looked at above:

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

#### To Have or Not Have State?

**Should this Component have state?**

**State** is optional. Since state increases complexity and reduces predictability, a component without state is preferable. Even though you can't do without state in an interactive app, you should avoid having many stateful components. Optimally, an app is comprised of mostly stateless components.

Often, apps are organized with higher level "container" components that manage state with multiple stateless components.

### Conclusion

- Stateless/presentational/presentational components deal with props only and don't have state or lifecycle methods.
- Stateful/container components manage state and props and deal with processing data that is changing over time.
- Best practice in writing clean code is to have mostly stateless components and a few stateful components.

#### References

* [JSPlayground](http://javascriptplayground.com/blog/2017/03/functional-stateless-components-react/)
* [Todd Motto](https://toddmotto.com/stateful-stateless-components)
* [Dan Abramov](https://medium.com/@dan_abramov/react-components-elements-and-instances-90800811f8ca)
