# React

## Install

Step | Command
---- | -------
Download and install Node.JS | Go to Node.JS site, download and install.
Install [create-ract-app](https://github.com/facebook/create-react-app) globally. Note: this has been updated in the official documentation. | `npm install create-react-app -g`
Create a project with this app. | `create-react-app my-app`
Enter the project. | `cd my-app`
Start app. | `npm start`

You need to import `react` and `react-dom`. You will need Babel as the JS preprocessor. Babel allows us to add HTML to JavaScript (JSX). It then compiles to normal JavaScript code.

## Sample Code

HTML

```
<div id="app"></div>
```

JavaScript

```
function Person(props) {
  return (
    <div className="person">
      <h1>{props.name}</h1>
      <p>Your Age: {props.age}</p>
    </div>
  );
}

var app = (
  <div>
    <Person name="Mike" age="31" />
    <Person name="Ricky" age="29" />
  </div>
  
);

ReactDOM.render(app, document.querySelector('#app'));
```

## Types of Applications

Single Page Applications | Multi Page Applications
------------------------ | -----------------------
Only one HTML page, content is (re)rendered on client. | Multiple HTML pages, content is rendered on server.
Typically only one ReactDOM.render() call. | One ReactDOM.render() call per widget.

## Folder Structure

Once `create-react-app` is created, you will have this folder structure.

- `package.json`: Stores metadata and dependency packages of the app.
- `node_modules`: Holds all the dependencies and subdependencies of the project. Don't edit it, it's automatically generated.
- `public`: Root folder that gets served by the web server. Holds the files we can edit.