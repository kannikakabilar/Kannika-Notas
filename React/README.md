<h1 style="color:#fc0303">React</h1>

<h3 style="color:#fc0303">Intro</h3>

> - <a style="color:#000000">Before writing React code, something needs to be imported in the \<head\> tag of index.html - Describe it</a>
> <br> A: react, react-DOM, babel must be imported through CDN using 3 script tags in index.html
>
> - <a style="color:#000000">Create a div element with id="root" in body tag. Create a script tag at the end of the \<body\> tag with type="text/babel". In that script tag, write a JS function called 'Hello' that returns a h1 html element. Write a statement that renders the 'Hello' function-element in the root div.</a>
>
> - <a style="color:#000000">There's another way to use React. How do you perform the setup? <br>
>       1) What do you need to have installed and how do you check if you have it installed? <br>
>       2) What is the command to create react app? <br>
>       3) cd into the newly created repo and how do you get it running on your local machine?</a>
>
> - <a style="color:#000000">In this newly created React app using node, where is the main react JS code written and where is the main html file located?</a>
> <br> A: When React renders a HTML element from src/index.js , it will be put in the "root" div element in public/index.html
>
> - <a style="color:#000000">What does JSX allow us to do in a JavaScript file? <br>
>       1) If you're assinging a html element to a JS variable, how could you put in some JS code like 5+5 in that html element? <br>
>       2) If you want to write a html element in multiple line and assign it to a JS varaible, how would you do that? <br>
>       3) How many html elements can you assign to a single JS variable?</a>
>

```html
<!DOCTYPE html><html>
    <head>
        <script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
        <script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>
        <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  </head>
  <body>
    <div id="mydiv"></div>
    <script type="text/babel">
      function Hello() {
        return <h1>Hello Kannika from HTML!</h1>;
      }
      ReactDOM.render(<Hello />, document.getElementById('mydiv'))
    </script>
  </body>
</html>
```

```shell
// Check if node and npm are installed
> node -v
> npm -v

// Command to create a react app
> npx create-react-app my-react-app

> cd my-react-app
> npm start
In browser, go to: http://localhost:3000/
```

```JSX
/* index.js */

// JSX allows us to write HTML directly in a JavaScript file

const myElement1 = <h1>React is {5 + 5} times better with JSX</h1>;

const myElement2 = (
  <ul>
    <li>Apples</li>
    <li>Bananas</li>
    <li>Cherries</li>
  </ul>
);

const myElement3 = (
  <>
    <p>I am a paragraph, but these paragraphs need to be one html element</p>
    <p>I am a paragraph too, which is within a fragment which look like empty html elements</p>
  </>
);

// Another way to perform the render
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(myElement1);
```

<h3 style="color:#fc0303">Components</h3>

> - <a style="color:#000000">What is a React Component? Component name must start with a ? Show what it is using a simple example.</a>
> <br> A: A React Component is a JavaScript function that returns a html element. Component/function name must start with a Captial Letter.
>
> - <a style="color:#000000">What are props in a React Component? Show an example that demonstrates the use of props.</a>
>
> - <a style="color:#000000">Write a React Component that calls another React Component</a>
>
> - <a style="color:#000000">Write a React Component in Car.js and export it. In index.js, import the component and render it.</a>

```JSX
/* React Component - Simple Example */
function Fruit() {
  return <h2>Hi, I am a Fruit!</h2>;
}
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Fruit />);

/* React Component - Props Example */
function Car(props) {
  return <h2>I am a {props.color} Car!</h2>;
}
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Car color="blue"/>);

/* Componet inside of a Component */
function Car() {
  return <h2>I am a Car!</h2>;
}
function Garage() {
  return (
    <>
      <h1>Who lives in my Garage?</h1>
      <Car />
    </>
  );
}
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Garage />);

/* Exporting and Importing Example */

/* src/Car.js */
function Car() {
  return <h2>Hi, I am a Car!</h2>;
}
export default Car;

/* src/index.js */
import React from 'react';
import ReactDOM from 'react-dom/client';
import Car from './Car.js';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Car />); 
```

<h3 style="color:#fc0303">Advanced Props</h3>

> - <a style="color:#000000">Props are arguments passed into React components. They are passed to components via HTML attributes. React Props are read-only! You will get an error if you try to change their value.</a>a>
>
> - <a style="color:#000000">Render a React Function-Element (React component) and pass in a object as one of its 'attribute' values</a>

```JSX
function Car(props) {
  return <h2>I am a { props.brand.model }!</h2>;
}

const root = ReactDOM.createRoot(document.getElementById('root'));
const carInfo = { name: "Ferrari", model: "Spider" };
root.render(<Car brand={ carInfo } />);                                //passing in objects are allowed and they must accessed properly in the function
```

<h3 style="color:#fc0303">Events</h3>

> - <a style="color:#000000">What is being referred to when React Events are mentioned?</a>
> <br> A: React has the same events as HTML: click, change, mouseover etc.
>
> - <a style="color:#000000">How is a React Event written differently compared to a HTML DOM event? Also, how is the event handler different in a Ract Event compared to a HTML DOM event?</a>
> <br> A: React events are written in camelCase syntax: onClick instead of onclick. React event handlers are written inside curly braces: onClick={shoot}  instead of onClick="shoot()".

```JSX
```