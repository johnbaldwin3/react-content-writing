## Getting Started with React
Getting started creating a React application is not too difficult when using the **Create React App** library available as a package on npm. We'll take a look at how install **Create React App** and generate an application. We will also take a look at a new language, *JSX*, which is used by most React applications to write markup.

### Create React App
**Create React App** is a library that helps us build React projects. It contains all of the tools that will take our React application and translate it into something the browser can understand. It also provides us with a development server (A local server that hosts a web application in development on a set port and watches for changes made to the code base, refreshing in the browser.). All of the libraries we need to make an application in React will be included.

#### Libraries included
- **Create React App** includes Webpack for module bundling. [^1]Webpack takes modules with dependencies and emits static assets representing those modules.
- [^2]Babel is the library that **Create React App** includes to compile ES2015 and later JavaScript into a browser-ready version of JavaScript.
- [^3]Autoprefixer is included to parse CSS and add vendor prefixes to rules.
- [^4]ESLint is included as a JavaScript linting utility.
- [^5]Jest is included as a JavaScript testing solution.

#### Installing
If you've chosen this course to become a React developer, this will be the beginning of many projects. There are tons of ways to create React applications and install of the needed dependencies. Let's look at a simple way using **Create React App**. We'll install it "globally" so that we need not install it every time we want to make a new React app.

The first step is to open up our terminal. It will not matter the directory we are in since we will be installing globally. On your command line, enter the following code:

``` bash
npm install -g create-react-app
```

It will take a few seconds to download all the tools. Once the download is done we're ready to start React.

#### Generating
Now that we've installed **Create React App** let's put it to use.

* The first step, **make sure you are now in your directory where you keep all of your projects**.
* There is no need to create a project folder, **Create React App** will do that for you, which is why we want to double check that we are in the directory that we want to create a project folder inside of.
* Once we are sure that we are in the right place, we can use the following command to initiate and create a React application.

``` bash
create-react-app the-name-of-my-application-here
```

*Just to clarify, after we type **Create React App**, we provide a space, and the name of the folder that we wish our application to be created inside of.*

* After this builds, we must actually open our project folder. We do so with the following code:

``` bash
cd the-name-of-my-application-here
```

* Once inside, we can open our project using our code editor, if using Atom, the following command will open our application. (Be sure you are inside of your project folder)

``` bash
atom .
```

Once Atom is launched, you'll see the layout of what was installed in your project folder. It should look something like this:

``` bash
my-app/
  README.md
  node_modules/
  package.json
  .gitignore
  public/
    favicon.ico
    index.html
  src/
    App.css
    App.js
    App.test.js
    index.css
    index.js
    logo.svg
```

[callout-info]It is important to note that when the `create-react-app` command runs, the name given to the folder is also used as the `name` property for your project in the newly created `package.json`.[/callout-info]

#### Development Server
We can now also open up our development server. The development server will track changes as we create our application. Each time we save our application the development server will automatically update in the browser and show us our changes.

To get the development server up and running we need to type the following command in the project folder:

``` bash
npm start
```

* The above command should open up a browser window with your project ready to go and watching for changes. If it doesn't open automatically, however, you can enter the following address in your browser "http://localhost:3000". We're now ready to start building our React app.

#### Monitoring Changes
React creates something called the "Virtual DOM". The Virtual DOM is a lightweight version of the DOM detached from the browser-specific implementation details. React works by constantly comparing the Virtual DOM to the actual DOM of our application. When React sees a change it automatically re-renders the application for us. Data being received, data being given by a user, interface animations, all of these change the DOM. React listens and renders the application accordingly.

### Translating HTML into JSX
Most common practice is to create an HTML page with one `<div id="root"></div>` inside the body of the HTML document. This `<div>` is the source for the entire application. That's really all of the HTML you are going to need to write. The rest of our project is going to be made up of components and JavaScript. The components are written in the language of JSX, which is XML syntax combined with JavaScript. It should be noted that you can use vanilla JavaScript to create components, but JSX makes the project much more streamlined, elegant and prevents us from directly incorporating vanilla HTML into our JavaScript files.

#### Demo App
Let's create a simple app to get started exploring React. We'll focus on the translation of HTML into JavaScript and how we tackle getting started with our **Create React App** format. Let's first look at boilerplate HTML below. This code is the beginnings of an application that allows you to input your favorite Bill Murray movie and displays something about it depending on what the input was.


``` html
<body>
  <nav class="navbar">
    <h1 class="title">Favorite Murray</h1>
  </nav>
  <main class="main-body">
    <div class="top">
      <div class="image-one">
        <img src="https://www.fillmurray.com/200/300" alt="Fill Murray Pictures">
      </div>
      <p class="top-paragraph">
        Lorem ipsum dolor sit amet, consectetur adipisicing.
      </p>
    </div>
    <div class="bottom">
      <div class="image-two">
        <img src="https://www.fillmurray.com/300/300" alt="Fill Murray Pictures">
      </div>
      <p class="bottom-paragraph">
        Lorem ipsum dolor sit amet, consectetur adipisicing.
      </p>
    </div>
  </main>
  <div class="murrayinator">
    <h3>What's your favorite Murray Movie?</h3>
    <form class="murray-form" action="" method="">
      <label for="murray-movie">Type your favorite movie here.</label>
      <input type="text" id="murray-movie">
      <button>Submit</button>
    </form>
  </div>
  <div class="answer">
    <h4 class="murray-display"></h4>
  </div>
  <script src="js/bundle.js"></script>
</body>
```

### Setup and Writing JSX
The three documents we'll focus on in our app are:

1. public/index.html
1. src/index.js
1. src/App.js

#### public/index.html
The only concern for us with HTML moving forward is the `<div></div>` in which our application will be inserted. **Create React App** has already provided us with HTML to get started and given us the following `<div>`:

``` html
<div id="root"></div>
```

That's all we need to know about this page. We won't write anything else in this document, but just know this is where React will yield our application.

#### src/index.js
This is our main JavaScript file. Inside of this file you'll see very little written already by our **Create React App** setup. We won't touch this file any further, but let's examine what's going on inside below.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import registerServiceWorker from './registerServiceWorker';
import './index.css';

ReactDOM.render(<App />, document.getElementById('root'));
registerServiceWorker();
```

Let's take a look at a few of the `import` statements at the top of this file. The first line imports React into our project. All React projects will begin with this import. The second line imports *ReactDOM*. ReactDOM is the glue that holds our React project and the DOM together. We use the ReactDOM to render our application and tell it where to insert itself into the DOM.

In our ReactDOM statement above you can see that we call:

```jsx
ReactDOM.render(<App />, document.getElementById('root'));
```

This line of code states that we want to use our `<App />` and insert it into the HTML page at the element with an ID of `root`. We've already looked at our HTML and saw the `<div id="root">` tag in the body. ReactDOM will render the `<App />` tag inside of the `<div id="root">`.

The 3rd line contains the importing of our app from the `src/App.js` file. This allows us to call our app inside the `index.js` and render it using ReactDOM.


#### src/App.js
The final piece of the puzzle is the `App.js` file. The `App.js` file has already been setup to get us started. Let's take a look at what's included below.

```html
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <div className="App-header">
          <img src={logo} className="App-logo" alt="logo" />
          <h2>Welcome to React</h2>
        </div>
        <p className="App-intro">
          To get started, edit <code>src/App.js</code> and save to reload.
        </p>
      </div>
    );
  }
}

export default App;
```


We're already familiar with classes and extending, as well as importing, so none of this should be too confusing. Let's break it down below so we can get started.

At the top, we import React, and the Component library from React in the first statement `import React, { Component } from 'react';`. We also import a logo and our style sheet, which we won't be covering in this lesson. The `App` class extends (inherits) from the React.Component library. We'll call a render method on that component, and return our first JSX.

* In a return statement a component can only render one div or piece of JSX. Everything must be contained within that div. Let's take a look below.

```jsx
return (
  <div></div>
  <div></div>
)
```

**The above code is invalid** because everything needs to be in one container. For what we're after, we can go ahead and delete everything so we're left with the following:

```html
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">

      </div>
    );
  }
}

export default App;
```

Since we are writing in JavaScript (JSX), reserved words such as `class` can not be used. If we want to give a class name to our JSX tags, they must be camelCased into `className`. In general, any HTML attributes will be camelCased in JSX. The HTML `for` attribute is also a reserved word in JavaScript, so it becomes `htmlFor`.

All single line tags such as `<img >` and `<input >` must become self-closing tags in JSX. In JSX all tags must have a closing tag or be self-closing. The two examples above would now be written as `<img />` and `<input />`. If you think back to our `index.js` file, you would notice that our `<App />` tag was self-closing too.

Let's see our app in JSX below.

```jsx
class App extends Component {
  render() {
    return (
      <div className="App">
        <nav className="navbar">
          <h1 className="title">Favorite Murray</h1>
        </nav>
        <main className="main-body">
          <div className="top">
            <div className="image-one">
              <img src="https://www.fillmurray.com/200/300" alt="Fill Murray Pictures" />
            </div>
            <p className="top-paragraph">
              Lorem ipsum dolor sit amet, consectetur adipisicing.
            </p>
          </div>
          <div className="bottom">
            <div className="image-two">
              <img src="https://www.fillmurray.com/300/300" alt="Fill Murray Pictures" />
            </div>
            <p className="bottom-paragraph">
              Lorem ipsum dolor sit amet, consectetur adipisicing.
            </p>
          </div>
        </main>
        <div className="murrayinator">
          <h3>What is your favorite Murray Movie?</h3>
          <form className="murray-form" action="" method="">
            <label htmlFor="murray-movie">Type your favorite movie here...</label>
            <input type="text" id="murray-movie" />
            <button>Submit</button>
          </form>
        </div>
        <div className="answer">
          <h4 className="murray-display"></h4>
        </div>
      </div>
    );
  }
}

export default App;

```

By exporting our `App` and then importing into our `index.js`, we can see the power of React in a Single Page Application. This lesson barely scratches the surface of what React has to offer, but hopefully, it demonstrates how easy it is to get started.

### Conclusion
* **Create React App** is installed with the `npm install -g create-react-app` command.
* To get a project started simply use the `create-react-app my-app-folder-name` command.
* After naming the folder, use the `cd my-app-folder-name` command to change into that directory.
* Use `npm start` to spin up your development server and watch for changes to your application.
* React most commonly uses JSX language to take the place of HTML.
* All React components will be rendered in a singular `<div>` on your `index.html` page.
* JSX requires camelCasing and special words to take place for reserved words such as "`class`" and "`for`" in JavaScript.

#### References
- [React Docs](https://facebook.github.io/react/docs/hello-world.html)
- [Create React App Docs](https://github.com/facebookincubator/create-react-app)
- [^1]: [Webpack](https://webpack.github.io/)
- [^2]: [Babel](https://babeljs.io/)
- [^3]: [Autoprefixer](https://github.com/postcss/autoprefixer)
- [^4]: [ESLint](http://eslint.org/)
- [^5]: [Jest](http://facebook.github.io/jest/)
