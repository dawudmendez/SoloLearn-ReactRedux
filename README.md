# SOLO LEARN - React + Redux

## Getting Started

### Front-End Development
- Front-end development refers to what the end user (also commonly referred to as the "client") can see. In the most basic forms, front-end development consists of HTML, CSS, and JavaScript.
- React uses a Virtual DOM, allowing to update only the parts of the website that have changed. This increases the speed

### Adding React to a Website
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

### Create React App
```bash
npx create-react-app my app
cd my-app
npm start
```
- This will install all the required dependencies, configure and start the project on localhost:3000

#### Project structure
- `public` (folder)
	- `index.html` <- HTML template of our page
- `src` (folder) <- contains all the JS, CSS and images that will be compiled into a bundle and injected into *index.html*
	- `index.js` <- entry point into our app, the method called *ReactDOM.render()* is used to find an element with id="root" in the HTML and add our app inside
	- `App.js` <- the main *component*

- The compilation is done by a *file loader*, which in this case is **Webpack**.
- It creates a bundle file that has the content of all that needs to be bundled together and it's all put into one file.

#### Changing the output
- We need to open src/index.js and change the code to the following:
```jsx
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <h1>Hello, React!</h1>
);
```

### Course Project
#### Contact Manager
- We'll create your own Contact Manager app using React.
- Code [here](https://stackblitz.com/edit/react-contact-manager-4?file=index.js)
