### Create React App

- A library that helps us build React projects. 
- Contains all of the tools that will take our React application and translate it into something the browser can understand. 
- Provides us with a development server (A local server that hosts a web application in development on a set port and watches for changes made to the code base, refreshing in the browser.).

#### Libraries included

- **Create React App** includes Webpack for module bundling. Webpack takes modules with dependencies and emits static assets representing those modules.
- Babel is the library that **Create React App** includes to compile ES2015 and later JavaScript into a browser-ready version of JavaScript.
- Autoprefixer is included to parse CSS and add vendor prefixes to rules.
- ESLint is included as a JavaScript linting utility.
- Jest is included as a JavaScript testing solution.

#### Installing


``` bash
npm install -g create-react-app
```

#### Generating


``` bash
create-react-app the-name-of-my-application-here
```

#### Development Server

``` bash
npm start
```

#### Virtual DOM

The Virtual DOM is a lightweight version of the DOM detached from the browser-specific implementation details. React works by constantly comparing the Virtual DOM to the actual DOM of our application. 

When React sees a change it automatically re-renders the application for us. Data being received, data being given by a user, interface animations, all of these change the DOM. React listens and renders the application accordingly.

### Translating HTML into JSX

Components are written in the language of JSX, which is XML syntax combined with JavaScript. 