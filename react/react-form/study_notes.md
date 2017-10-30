## Implementing a Form on a React Component

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
        <input type="submit" value="Submit"/>
      </form>
    )
  }
}
```
