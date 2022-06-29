# Getting Started

## Front-End Development
- Front-end development refers to what the end user (also commonly referred to as the "client") can see. In the most basic forms, front-end development consists of HTML, CSS, and JavaScript.
- React uses a Virtual DOM, allowing to update only the parts of the website that have changed. This increases the speed

## Adding React to a Website
- React can be added to a website without any special tools and installations.
- First, we need to add the React library as two script tags to the head of our HTML document:
```html
<script src="https://unpkg.com/react@16/umd/react.development.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js" crossorigin></script>
```
- Next, we need to add another script, to enable the use of JSX.
- JSX is a syntax extension to JavaScript, and it is recommended to be used with React.
```html
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```
- After adding the required script tags, we can start building our React app.
- We add a container, that will be used to display something using React.
```html
<div id="container"></div>
```
- Let's display a simple message as a heading:
```jsx
<script type="text/babel">
ReactDOM.render(
  <h1>Hello, React!</h1>,
  document.getElementById('container')
)
```

## Create React App
```bash
npx create-react-app my app
cd my-app
npm start
```
- This will install all the required dependencies, configure and start the project on localhost:3000

### Project structure
- `public` (folder)
	- `index.html` <- HTML template of our page
- `src` (folder) <- contains all the JS, CSS and images that will be compiled into a bundle and injected into *index.html*
	- `index.js` <- entry point into our app, the method called *ReactDOM.render()* is used to find an element with id="root" in the HTML and add our app inside
	- `App.js` <- the main *component*

- The compilation is done by a *file loader*, which in this case is **Webpack**.
- It creates a bundle file that has the content of all that needs to be bundled together and it's all put into one file.

### Changing the output
- We need to open src/index.js and change the code to the following:
```jsx
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <h1>Hello, React!</h1>
);
```

## Course Project
### Contact Manager
- We'll create your own Contact Manager app using React.
- Code [here](https://stackblitz.com/edit/react-contact-manager-4?file=index.js)

# Intro to React
## JSX
### What is JSX?
```jsx
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <h1>Hello, React!</h1>
);
```
- The element is not in quotes to represent a string.
- It's like an HTML element, however we use it right in the JavaScript code.
- This is called JSX, and it is a syntax extension to JavaScript.
- It allows us to build UI elements right in the JavaScript code.
- React does not require using JSX, however, it is common practice to use it.

### Intro to JSX
In this case (which didn't work):
```jsx
ReactDOM.render(
  <h1>Hello, React!</h1>,
  document.getElementById('root')
);
```
- The code calls React's render method, and passes it two arguments, a JSX element and a container.
- The render method displays the provided element in the container, which, in our case, is the HTML element with id="root".

### Expressions in JSX
- We can use any JavaScript expression inside JSX using curly braces.
```jsx
const name = "Dawud";
const el = <p>Hello, {name}</p>;

ReactDOM.render(
  el,
  document.getElementById('root')
);
```

### Attributes in JSX
- We can specify attributes using quotes, just like in HTML:
```jsx
<div id="name"></div>
```
- When using a JavaScript expression as the attributes value, the quotes should not be used:
```jsx
<div id={user.id}></div>
```

## Virtual DOM
### How Does JSX Work?
- When the JSX expressions are compiled, they are converted into JavaScript objects, representing React elements.
- React then uses these elements to build the corresponding HTML DOM and display it in the browser.
- Example app that increments a counter variable every second and displays it on the page as a paragraph:
```jsx
let counter = 0;

function show() {
  counter++;
  const el = <p>{counter}</p>;
  ReactDOM.render(
    el, document.getElementById('root')
  );
}

setInterval(show, 1000);
```
- We use setInterval to call the show function every second and render the counter element on the page.

### Virtual DOM
- React uses a Virtual DOM, which is a lightweight representation of the DOM.
- When an element gets changed, it is first updated in the Virtual DOM. That process is fast, as the virtual DOM is represented by simple objects.
- After that, React compares the Virtual DOM to its previous state and only applies the DOM updates necessary to bring the DOM to the desired state.

## Components
### Components
- Let you split the page into independent and reusable parts.
- The heading is a component, the "new question" button is a component, and the search bar is its own component.
- This makes organizing the page leaps and bounds easier, but even more importantly, components allow us as the developers to separate concerns from one another.

### Functional Components
- In React, there are two types of components that you can use: Functional Components and Class Components.
- A functional component is a simple JavaScript function:
```jsx
function Hello() {
  return <h1>Hello world.</h1>;
}
```
- The code above defined a functional component called Hello, that returns a simple React element.
- The name of the functional component begins with a capital letter. This is absolutely critical.

### Rendering Components
- In order to display the component, we need to create the corresponding JSX element.
- For example, for our user-defined component Hello:
```jsx
const el = <Hello />;
```
- Now, we can use our user-defined element and render it on the page:
```jsx
function Hello() {
  return <h1>Hello world.</h1>;
}

const el = <Hello />; 
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  el
);
```

### Class Components
- Class components are typically used when there are more advanced user interactions, like forms, and animations.
- All class components need to extend the React.Component class.
- We can rewrite our Hello functional component as a class component:
```jsx
class Hello extends React.Component {
  render() {
    return <h1>Hello world.</h1>;
  }
}
```

## Props
### Props
- Functional components can accept arguments, similar to JavaScript functions. These arguments are called props, and represent an object.
- For example, we can use props in our Hello component:
```jsx
function Hello(props) {
  return <p>Hello, {props.name}!</p>;
}
```
- Now, we can add a name attribute to our element:
```jsx
const el = <Hello name="Dawud" />; 
```
- The attribute value will be passed to the component when rendered.

### Components using Components
- Components can use other components to generate an output.
```jsx
function App() {
  return <div>
    <Hello name="David" />
    <Hello name="James" />
    <Hello name="Amy" />
  </div>;
}
```
- Here, our App component uses the Hello component three times, each times with a new name attribute.

### Props in Class Components
- Props can be accessed in class components using this.props.
```jsx
class Hello extends React.Component {
  render() {
    return <p>Hello, {this.props.name}!</p>;
  }
}
```
- An important thing to consider is that props are read-only, meaning components cannot modify their props.

### An Example
- Let's create a shopping list.
- Each item in our list will have a name and a price.
```jsx
<Item name="Cheese" price="4.99" /> 
```
- The Item component will render a simple div element with the data:
```jsx
function Item(props) {
  return <div className="item">
  <b>Name:</b> {props.name} <br />
  <b>Price:</b> {props.price}
  </div>;
}
```
- Now we can use our component and create multiple items for our shopping list:
```jsx
<Item name="Cheese" price="4.99" />
<Item name="Bread" price="1.5" />
<Item name="Ice cream" price="24" />
```

## State
### State
- Props cannot be changed.
- In order to allow components to manage and change their data, React provides a feature called state.
- State is an object that is added as a property in class components.
- It contains key:value pairs.
- Similar to props, the values can be accessed using this.state.
```jsx
class Hello extends React.Component {
  state = {
    name: "James"
  }

  render() {
    return <h1>Hello {this.state.name}.</h1>;
  }
}
```
- Now, when the component renders, the state is initialized with the given value and there will be a heading that says "Hello James.".

### Changing State
- State should not be modified directly.
- Instead, React provides a setState() method, that can be used to modify state.
```jsx
this.setState({ 
  name: "James",
  age: 25
}); 
```
- You need to pass an object with the new key:value pairs to the setState method.
- Why should we use setState, instead of simply changing the values of the object properties directly?
The answer uncovers one of the most useful features of React: when setState is called, React automatically re-renders the affected component with the new state!
- Usually, the change in state happens in event handlers.

### Counter App
- Let's create a counter app, which increments the counter each time a button is clicked.
- We start by creating our Counter component, which includes the counter and a button:
```jsx
class Counter extends React.Component {
  state = {
    counter: 0
  }
  render() {
    return <div>
    <p>{this.state.counter}</p>
    <button>Increment</button>
    </div>;
  }
} 
```
- We have initialized our counter to the value 0 in the state.
- Now, we need to add a click event handler to the button and increment the counter in the state.
```jsx
class Counter extends React.Component {
  state = {
    counter: 0
  }
  increment = () => {
    this.setState({
     counter: this.state.counter+1});
  }
  render() {
    return <div>
    <p>{this.state.counter}</p>
    <button onClick={this.increment}>Increment</button>
    </div>;
  }
}
```
- The onClick event calls the increment function of our component, which uses setState to change the value of our counter.
- When the state is changed, React automatically triggers a re-render of the component.

### Prop vs State
- We use props to pass data to components.
- Components use state to manage their data.
- Props are read-only and cannot be modified.
- State can be modified by its component using the setState() method.
- The setState() method results in re-rendering the component affected.

## Hooks
### Hooks
- They allow us to use state inside of functional components.
- First, we need to import the useState hook:
```jsx
import React, { useState } from 'react';  
```
- useState returns a pair, the current state value and a function, that lets you change the state.
- useState takes one argument, which is the initial value of the state.
```jsx
function Hello() {
  const [name, setName] = useState("Dawud");

  return <h1>Hello {name}.</h1>;
} 
```
- We create a name state variable and a setName function.
- The square brackets syntax is called array destructuring.
- It assigns the name variable to the current state value, and setName to the function that allows to change the state.
- You can name these variables anything you like.
- Then, we pass "Dawud" as the initial value for our name variable to useState()

### Counter App using Hooks
```jsx
function Counter() {
  const [counter, setCounter] = useState(0);

  function increment() {
    setCounter(counter+1);
  }

  return <div>
  <p>{counter}</p>
  <button onClick={increment}>
    Increment
  </button>
  </div>;
}
```

### Lifecycle Methods
- Special methods for *class components*
- Called when components are mounted, updated or unmounted
- Mounting is the process when a component is rendered on the page.
- Unmounting is the process when a component is removed from the page.
- The componentDidMount method is called when a component is rendered on the page.
- For example, we can use componentDidMount in our Counter app to set the initial value of the counter:
```jsx
componentDidMount() {
  this.setState({counter: 42});
}
```
- This will set an initial value of the counter when the component is rendered.
- componentDidMount is typically used for populating the state inside of a component when it initially mounts to the DOM.

### componentDidUpdate
- Called when a component is updated in the DOM.
- We can, for example, alert the current counter value when it is incremented:
```jsx
componentDidUpdate() {
  alert("Number of clicks: " + this.state.counter);
}
```

### The useEffect Hook
- The lifecycle methods we covered are only available for class components.
- There is a special Hook called useEffect for functional components.
- It combines the componentDidMount, componentDidUpdate, and componentWillUnmount methods into one.
```jsx
function Counter() {
  const [counter, setCounter] = useState(0);

  useEffect(() => {
    alert("Number of clicks: " + counter);
  });

  function increment() {
    setCounter(counter+1);
  }
  return <div>
  <p>{counter}</p>
  <button onClick={increment}>Increment</button>
  </div>;
}
```
- By default, useEffect runs both, after the first render and after every update.
- To call the method only when something changes, we can provide it a second argument:
```jsx
useEffect(() => {
  //do something
}, [count]);  
```
- Now, the useEffect() method will run only if count changes.
- To mimic componentWillUnmount, useEffect may return a function that cleans up after it:
```jsx
useEffect(() => {
  // do something
  
  return () => {
    // cleanup
  }; 
});
```
- You can have multiple effects in the same component.

## Handling Events
### Event Handling
```jsx
<button onClick={handleClick}>
  My Button
</button>
```
- Clicking the button will call the handleClick function of the component.
```jsx
function Counter() {
  const [counter, setCounter] = useState(0);

  function increment() {
    setCounter(counter+1);
  }
  return <div>
  <p>{counter}</p>
  <button onClick={increment}>Increment</button>
  </div>;
}
```
- The onClick event calls the increment function, which is incrementing the counter state variable.

### Handling User Input
- We can handle user input in React using the onChange event of the text field.
- When the value of the text field changes, the event handler is called, updating the value of the field in the component's state.
```jsx
function Converter() {
  const [km, setKm] = useState(0);

  function handleChange(e) {
    setKm(e.target.value);
  }
  function convert(km) {
    return (km/1.609).toFixed(2);
  }

  return <div>
  <input type="text" value={km}
     onChange={handleChange} />
  <p> {km} km is {convert(km)} miles </p>
  </div>;
}
```
- Our Converter component includes a text field, which calls the handleChange function when its value changes.
- The handleChange function updates the state with the current value of the textfield, causing the component to re-render and show the corresponding miles value, which is calculated using the convert function.

### Forms
- React form elements keep their state and update it based on user input.
- You always have the data of your form at your disposal in the state.
```jsx
function AddForm() {
  const [sum, setSum] = useState(0);
  const [num, setNum] = useState(0);

  function handleChange(e) {
    setNum(e.target.value);
  }

  function handleSubmit(e) {
    setSum(sum + Number(num));
    e.preventDefault();
  }

  return <form onSubmit={handleSubmit}>
  <input type="number" value={num} onChange={handleChange} />
  <input type="submit" value="Add" />
  <p> Sum is {sum} </p>
  </form>;
}
```
- In the code above, the value of the input is controlled by React (we keep the value in the state).
- When the form is submitted using the submit button, the handleSubmit function gets called, which updates the value of sum in the state.
- An input form element whose value is controlled by React in this way is called a "controlled component".

## Rendering A List
### Lists
```jsx
const arr = ["A", "B", "C"];
```
- We need to render a list <li> element for each item in the array.
- We can define a MyList component and pass it the array as a prop using a custom data attribute:
```jsx
<MyList data={arr} />
```
- Now, when the array is accessible via props, we can write the component logic:
```jsx
function MyList(props) {
  const arr = props.data;
  const listItems = arr.map((val) =>
    <li>{val}</li>
  );
  return <ul>{listItems}</ul>;
}
```
