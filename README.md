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
- We need to render a `<li>` element of each item in the array.
- We can define a **MyList** component and pass it the array as a prop using a custom **data** attribute:
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

### Keys
- Each element in a list must have a key attribute.
- Keys act as a unique identity, identifying each element.
- Usually, these are IDs from your data, or can be auto-generated indexes.
```jsx
const listItems = arr.map((val, index) =>
  <li key={index}>{val}</li>
);
```

### Contact Manager
![App](https://api.sololearn.com/DownloadFile?id=4390)
- By looking at the mockup, it makes sense to have two components:
	- **AddPersonForm**: a form with the text field and Add button.
	- **PeopleList**: a list of contacts.

#### AddPersonForm
- Uses state to manage the value of the text field:
```jsx
function AddPersonForm() {
  const [ person, setPerson ] = useState("");

  function handleChange(e) {
    setPerson(e.target.value);
  }

  function handleSubmit(e) {
    e.preventDefault();
  }
  return (
    <form onSubmit={handleSubmit}>
    <input type="text" 
    placeholder="Add new contact" 
    onChange={handleChange} 
    value={person} />
    <button type="submit">Add</button>
    </form>
    );
}
```
- For now, we just prevent the default behavior when the form is submitted.

#### PeopleList
- Received an array representing the contacts and renders a list on the page:
```jsx
function PeopleList(props) {
  const arr = props.data;
  const listItems = arr.map((val, index) =>
    <li key={index}>{val}</li>
  );
  return <ul>{listItems}</ul>;
}
```

#### Rendering both components
```jsx
const contacts = ["James Smith", "Thomas Anderson", "Bruce Wayne"];

const el = (
  <div>
    <AddPersonForm />
    <PeopleList data={contacts} />
  </div>
);
```

### Sharing State
- Right now, our AddPersonForm independently keeps its state.
- How can we add a new contact to our PeopleList then, when the form is submitted?
- We can do that by lifting the state up to a parent component.
- Let's create a parent component called **ContactManager**, which includes the **AddPersonForm** and **PeopleList** as child components and holds the contacts list in its state:
```jsx
function ContactManager(props) {
  const [contacts, setContacts] = useState(props.data);

  return (
    <div>
      <AddPersonForm />
      <PeopleList data={contacts} />
    </div>
  );
} 
```
- Data can be passed from the parent to the child, but not from the child to the parent.
- React uses what is called **unidirectional data flow**, in other words, data only flows downward, so to speak.

### Adding a Contact
- Now, we can create an **addPerson()** function to our ContactManager component to add a new person to our contacts state array:
```jsx
function ContactManager(props) {
  const [contacts, setContacts] = useState(props.data);

  function addPerson(name) {
    setContacts([...contacts, name]);
  }
 ...
}
```
- We can pass a function reference to another component
```jsx
function ContactManager(props) {
  const [contacts, setContacts] = useState(props.data);

  function addPerson(name) {
    setContacts([...contacts, name]);
  }

  return (
    <div>
      <AddPersonForm handleSubmit={addPerson} />
      <PeopleList data={contacts} />
    </div>
  );
}
```
- We passed down the addPerson() function to our AddPersonForm using a prop called handleSubmit.
- Now, our PeopleList can call the handleSubmit function that it received when the form is submitted, to add a new person to the list:
```jsx
function AddPersonForm(props) {
  const [ person, setPerson ] = useState('');
    
  function handleChange(e) {
    setPerson(e.target.value);
  }
    
  function handleSubmit(e) {
    props.handleSubmit(person);
    setPerson('');
    e.preventDefault();
  }
  return (
    <form onSubmit={handleSubmit}>
      <input type="text" 
        placeholder="Add new contact" 
        onChange={handleChange} 
        value={person} />
      <button type="submit">Add</button>
    </form>
  );
}
```

# Intro to Redux
## State Management
### Introducing Redux
- Redux was created to make state management predictable, providing a single state container and strict rules on how state can be changed.
- Redux is a small JavaScript library and can be used with any front-end framework, such as React, Angular, jQuery.
- It employs the "single source of truth" pattern.
- In short, single source of truth just refers to relocating the application state and all associated logic outside of the application, allowing ANY component to access the data it needs.

## Core Concepts
### Store
- In Redux, the application's state is stored as a simple object, called store.
- There should only be a single store in an app.
- For example, a store can look like this:
```jsx
{
  contacts: [{
    name: 'David'
  }, {
    name: 'Amy'
  }],
  toggle: true
}
```
- You cannot change the state directly. Instead, you need to dispatch an action.

### Actions & Reducers
- An action is just a plain JavaScript object:
```jsx
{ 
  type: 'ADD_CONTACT', 
  name: 'James' 
}
```
- The code above defines an action with type ADD_CONTACT and a name property.
- An action clearly describes why the state change happened, and can be dispatched from anywhere in your app.
- To tie the store and the action together, we need to write a function, called a reducer.
- It takes state and action as arguments, and returns the next state of the app.
```jsx
function contactsApp(state, action) {
  if (action.type === 'ADD_CONTACT') {
    return [ ...state,  action.name ]
  } else {
    return state
  }
}
```
- The code above defines a simple reducer function, that checks the action and returns the new state.
- We have not touched any React specific syntax, all of the above is plain JavaScript.

### Core Concepts
Redux can be described using the following principles:
- **Single source of truth**: The global state of the app is stored in a single store.
- **State is read-only**: You can change the state only by dispatching actions. Action are objects, that contain information about what should be changed.
- **Pure reducers**: Reducers are functions that handle the actions and return the next state of the application. Reducers need to be pure, meaning they cannot modify the state, they need to return a new state object.

## Actions
- Action can be viewed as payloads of information that send data to the store.
- Actions are represented by simple JavaScript object and need to have a type property:
```jsx
{
  type: 'ADD_CONTACT',
  name: 'James'
}
```
- In the example above, we define an action with the type ADD_CONTACT and provide it a name property as its payload.
- Note that the action type needs to be in upper snake case.
- You can use any naming and structure for the other properties defining the data in the action.
```jsx
{
    type: 'ADD_CONTACT',
    payload: {
        name: "Jimmy Barnes"
    }
 }
```
- You should pass as little data in each action as possible. That keeps the actions clean and easy to read.

### Action Creators
- In order to use the same action with different payloads, as well as create reusable code, we can create Action creators.
- Action creators are simple functions that return actions.
```jsx
function addContact(person) {
  return {
    type: 'ADD_CONTACT',
    payload: person
  }
}
```
- The action creator function takes a person parameter and uses that as the actions payload.
- Now, we can use the action creator to create multiple new contacts by passing it the corresponding data.
- Action creators are not built into the Redux library by default. It is a pattern that was implemented to create code that reflects a more DRY (Don't Repeat Yourself) approach.

### Reducers
- Reducers are functions that handle the actions.
- The function takes the current state and the action as its parameters and returns the new state.
- A reducer can handle multiple actions, so usually it includes a switch statement for each action case.
```jsx
function contactsApp(state, action) {
  switch (action.type) {
    case 'ADD_CONTACT':
      return [ ...state,  action.person ]
    default:
      return state
  }
}
```
- In the code above, our reducer function uses a switch statement to handle the appropriate actions.
- As the default case, it just returns the current state.
- Remember, the reducer has to be a pure function, meaning it cannot modify the current state. It has to return a new state object instead.
- The default case is added for handling unknown actions.

### Multiple Reducers
- If you have more than one entity (i.e. users, products, invoices, orders, etc.), it's typically a good idea to break them into multiple reducer functions to separate concerns.
- Redux gives us a method that we can use called combineReducers.
- This allows us to use more than one reducer so that when an action gets dispatched, the action would get run through all of the reducers instead of only one.
- It also allows us to separate the concerns of our store state.
```jsx
const contactsApp = combineReducers({
  addContacts,
  doSomething
})
```
- Now, our contactsApp is combining two reducers into one.
- It's a good practice to provide each reducer only the part of the state that it needs to manage. This is called **reducer composition**, and is a fundamental pattern of building Redux apps.

### Redux with React
- First, we need to install Redux:
```bash
npm install redux 
```
- To use it with React, we need to install another library, called react-redux:
```bash
npm install react-redux
```
- The react-redux library binds React with Redux, allowing React components to read data from a Redux store, and dispatch actions to the store to update data.

### Counter App
- As our first example, let's build the **Counter** app we made in the previous module using Redux!
- First, we need to create our action and corresponding _reducer_.
```jsx
const initialState = {
  count: 0
};

function reducer(state = initialState, action) {
  switch(action.type) {
    case 'INCREMENT':
      return { count: state.count + action.num };
    default:
      return state;
  }
}
```
- The code above defines a reducer function, which returns the new state based on the given action. We increment the count state variable by the provided num value.
- We also provide a default value for our state using the initialState variable.

### Creating the Store
- To create the store, we call the createStore() function, which takes the reducer as its parameter:
```jsx
const store = createStore(reducer);
```
- But how do we pass the store to our components?
- That is achieved using a special `<Provider>` element. It makes the store available to any nested child component.
- So, for our counter, we would have the following:
```jsx
const el = <Provider store={store}>
    <Counter/>
  </Provider>; 
```
- Provider takes the store as an attribute and makes it available to its child component.
- We need to import `{ createStore }` and `{ Provider }` using the following syntax:
```jsx
import { Provider } from 'react-redux';
import { createStore } from 'redux';
```

### Connecting to the Store
- At this point, we have created our action, the reducer, the store, and made it available to our Counter component using the Provider element.
- In order to connect our component to the store, we need to call the connect() function.
- The connect() function returns a new component, that wraps the component you passed to it and connects it to the store using its special parameter functions.
```jsx
function connect(mapStateToProps?, mapDispatchToProps?) 
```
connect() takes two optional parameters:

#### mapStateToProps
- This function is called every time the store state changes. It receives the state as a parameter and returns the state for the component.
- For example, for our Counter, we need to return the count state variable:
```jsx
function mapStateToProps(state) {
  return {
    count: state.count
  };
}
```
- Now, our component can access the **count** variable using its **props**.
- Just as the name of the function states, it maps the state to the props.

#### mapDispatchToProps
- As you may have guessed from the name, this parameter is used to map the dispatch functions to props.
- It can be a simple object, defining the function that needs to be mapped:
```jsx
const mapDispatchToProps = {
  incrementCounter
}
```
- This might seem a bit confusing, but its very straightforward: **mapStateToProps** simply returns the state variables as props to our component, while **mapDispatchToProps** allows to define how we dispatch actions and make the dispatching functions available as props.
- **mapDispatchToProps** can also be defined as a function. Take a look at the [official documentation](https://react-redux.js.org/using-react-redux/connect-mapdispatch) for more details.
- Note that we need to import the connect function:
```jsx
import { connect } from 'react-redux';
```

### Accessing The Store
- Inside our component we just access the store properties using props
```jsx
function Counter(props) {
  function handleClick() {
    props.incrementCounter(1);
  }
    return <div>
    <p>{props.count}</p>
    <button onClick={handleClick}>Increment</button>
    </div>;
}
```
- Notice, that we pass 1 as the argument to our **incrementCounter()**, making our counter increment by 1. 
- We can change the value to any other number, and our counter will behave as expected, because we handled the increment parameter in our reducer.
- Now, the only thing left is to call the connect() function for our Counter component and render it on the page:
```jsx
const Counter = connect(mapStateToProps, mapDispatchToProps)(Counter);

const el = <Provider store={store}>
          <Counter/>
        </Provider>;
```

### Project Structure
- We can move our Counter component and the action creator function to a separate Counter.js file.
- In order to use the Counter component in our index.js, we need to export it first:
```jsx
export default connect(mapStateToProps, mapDispatchToProps)(Counter);
```
 - Notice, we export the connected component.
 - Now, we can import the component in index.js:
 ```jsx
import Counter from './Counter'; 
```
- We use the _ES6 modules system_, which allows use to export and import modules.
