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

```jsx
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
> <br> A: A React Component is a JavaScript function that returns a JSX element (which is like a html element but can contain some embedded JS code). Component/function name must start with a Captial Letter.
>
> - <a style="color:#000000">What are props in a React Component? Show an example that demonstrates the use of props.</a>
>
> - <a style="color:#000000">Write a React Component that calls another React Component</a>
>
> - <a style="color:#000000">Write a React Component in Car.js and export it. In index.js, import the component and render it.</a>
>
> - <a style="color:#000000">What is meant by composability in React?</a>
> <br> A: React components can be separated into different files (ie: Header of webpage can be store in Header.js and imported into App.js, Footer of webpage can be stored in Footer.js and imported and same for Navbar and MainContent and so on) and they can all be imported and rendered toether in App.js
>
> - <a style="color:#000000">How do you import a .css file in React (ie: Try to import App.css)</a>

```jsx
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
import "./App.css"

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Car />); 
```

<h3 style="color:#fc0303">Advanced Props</h3>

> - <a style="color:#000000">Props are arguments passed into React components. They are passed to components via HTML attributes. React Props are read-only! You will get an error if you try to change their value.</a>
>
> - <a style="color:#000000">Render a React Function-Element (React component) and pass in a object as one of its 'attribute' values</a>

```jsx
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
>
> - <a style="color:#000000">Task: Write a React Event </a> <br>
>             - Create a React Component function called Football (it doesn't take any args) <br>
>             - Inside the Football function, create an arrow function called 'shoot', that takes in two args. <br>
>             - Inside the arrow function, it should alert a message that displays the value of both the args. <br>
>             - Return a button element in the Footbal function React Component. <br>
>             - This button should have an event called 'onClick' and its event handler is an arrow function that takes in 'e' representing event <br>
>             - In the body of the arrow function inside the event handler of the button, call shoot and send in args: "Goal!" and the event type (how do you send in even type?) <br>
>             - Render the Football function-ReactComponent <br>

```jsx
function Football() {
  const shoot = (a, b) => {
    alert(a + ' action was done by ' + b);
  }
  return (
    <button onClick={(event) => shoot("Goal!", event.type)}>Take the shot!</button>
  );
/*
'event' represents the React event that triggered the function - In this case, the 'click' event
 output: Goal! action was done by click
*/
}
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Football />);
```

<h3 style="color:#fc0303">Rendering Lists</h3>

> - <a style="color:#000000">Say you have a JS list filled with names. If you want to render a list of items using li tag in ul onto the webpage, you cannot write a for-loop inside {} (curly brackets), what method do you use in the curly bracket?</a>
>
> - <a style="color:#000000">When you are rendering the same React Component function-element multiple times, you need to pass-in a specific attribute, that can only be passed-in and not accessed, what is it? and why do you need to pass it in?</a>
> <br> A: Keys allow React to keep track of elements. This way, if an item is updated or removed, only that item will be re-rendered instead of the entire list. Generally, the key should be a unique ID assigned to each item.

```jsx
function Car(props){
  return <li>I am a { props.brand }</li>        // props.key cannot be accessed here, if id is needed => pass it in as a separate prop
}

function Garage() {
  const cars = [                   // it is a convention to use id as keys in the data type
    {id: 1, brand: 'Lambo'},
    {id: 2, brand: 'BMW'},
    {id: 3, brand: 'Audi'}
  ];
  return (
    <>
      <h1>Who lives in my garage?</h1>
      <ul>
        {
          cars.map((car) => <Car key={car.id} brand={car.brand} />)    // key prop needs to be passed-in to differentiate between multiple Car React-Components
        }
      </ul>
    </>
  );
}
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Garage />);
```

<h3 style="color:#fc0303">Hooks</h3>

> - <a style="color:#000000">Before using Hooks, what needs to be done first?</a>
> <br> A: You must first import each specific hook before using it.

<h3 style="color:#fc0303">UseState Hooks</h3>

> - <a style="color:#000000">What is the useState used for?</a>
> <br> A: useState Hook allows us to track state (of a property) in a function component.
>
> - <a style="color:#000000">What 1 value is inputted into the useState function and what 2 values are outputted? Show an example using useState.</a>
> <br> A: The 1 input value is the inital value that is set for the prop and it returns a variable containing the current value and a fucntion that takes in new value to update the current value stored in the variable returned as first result. (check example for clarity)
>
> - <a style="color:#000000">useState can be used to track a combination of values. Explain how and if you only want to change one value from an object show how that's done</a>
>
> - <a style="color:#000000">You have 2 options for what you can pass in to a state setter function (e.g. `setCount`). What are they?</a>
> <br> A: The new value of state (ie: count) or a function that is executed with previous state value as its arg and the return value is stored as the new value of state.

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import { useState } from "react";

function FavoriteColor() {
  const [color, setColor] = useState("red");    //This is called Destructuring: assigning the return values to 2 different vars

  return (
    <>
      <h1>My favorite color is {color}!</h1>
      <button
        type="button"
        onClick={() => setColor("blue")}    // using the setColor funtion returned from useState to update the value of color
      >Blue</button>
    </>
  )
}
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<FavoriteColor />);

function Car() {
  const [car, setCar] = useState({    // using useState to track an object
    brand: "Lambo",
    model: "Aventador",
    year: "2017",
    color: "white"
  });

  const updateColor = () => {
    setCar(previousState => {    // using setCar function to only change the color - making use of JS spread operator
      return { ...previousState, color: "blue" }
    });
  }

  return (
    <>
      <h1>My {car.brand}</h1>
      <p>
        It is a {car.color} {car.model} from {car.year}.
      </p>
      <button
        type="button"
        onClick={updateColor}
      >Blue</button>
    </>
  )
}
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Car />);
```

<h3 style="color:#fc0303">UseEffect Hooks</h3>

> - <a style="color:#000000">What is useEffect used for?</a>
> <br> A: Syncing 2 different internal states, though specific states get update when its value changes, some state values must be synced and need to get updated together. Also when props or local variable changes sometimes the page needs to get re-rendered. => useEffect can be used for this.
>
> - <a style="color:#000000">The function in useEffect will get executed AT LEAST how many times?</a>
> <br> A: It will get executed at least once during the first initial render (regardless of the 2nd arg), and the number of times it renders after that depends on the 2nd arg.
>
> - <a style="color:#000000">What are the 3 different values you can pass-in for the 2nd arg for useEffect? and how do they work?</a><br>
>     - No (2nd arg) dependency passed: useEffect(() => { //Runs on every render (a render occurs everytime any state value changes) }); <br>
>     - Empty array (as 2nd arg) passed: useEffect(() => { //Runs only on the first render }, []); <br>
>     - Props passed (for 2nd arg): useEffect(() => { //Runs on the 1st render and any time a dependency value stated in the 2nd arg's array changes }, \[prop, state\]); <br>
>
> - <a style="color:#000000">Create a state value called 'count' and set its initial value to 0. Now, create a useEffect where its 1st arg function executes during every render. For the 1st arg, create an arrow function whose body calls setTimeout. The 1st arg of the setTimeout function should be executed every 1000ms. Create another arrow function for the 1st arg of the setTimeout which calls for 'setCount' and increments previous count value by 1.</a>

```jsx
import { useState, useEffect } from "react";
import ReactDOM from "react-dom/client";

function Timer() {
  const [count, setCount] = useState(0);

  // write the useEffect here


  return <h1>I've rendered {count} times!</h1>;
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Timer />);
```

> - <a style="color:#000000">Example 2: Doubler - Create a useEffect that will set the 'calculation' value as twice the count value everytime the value of 'count' changes</a>

```jsx
import { useState, useEffect } from "react";
import ReactDOM from "react-dom/client";

function Counter() {
  const [count, setCount] = useState(0);
  const [calculation, setCalculation] = useState(0);

  // create a useEffect here that will set the 'calculation' value as twice the count value everytime the value of 'count' changes

  return (
    <>
      <p>Count: {count}</p>
      <button onClick={() => setCount((c) => c + 1)}>+</button>
      <p>Calculation: {calculation}</p>
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Counter />);
```

> - <a style="color:#000000">Fetching data from API  and setting the result to a state value needs to be placed where in a react code?</a>
> <br> A: Inside the useEffect function with an empty array as its second arg so that it doesn't infinitely keep rendering itself.
>
> - <a style="color:#000000">Example 3: Make a fetch request in useEffect to this api: 'https://www.boredapi.com/api/activity' and set the result to 'activity' state. The fetch request should only be executed once</a>

```jsx
import React from "react"

export default function App() {
    const [activity, setActivity] = React.useState("")
    
    
    // This useEffect handles the promise resulted from fetch request and assigns it to 'activity' state
    React.useEffect(function() {
        fetch("https://www.boredapi.com/api/activity")
            .then(res => res.json())
            .then(data => setActivity(data.activity))
    }, [])

    // The fetch request (that is inside the 1st arg function of useEffect) is executed only once
    // If the fetch request was placed outside the useEffect, it would cause infinite rendering
    
    return (
        <div>
            <pre>You should: {JSON.stringify(activity)}</pre>
        </div>
    )
}
```

> - <a style="color:#000000">Example 4: EventListeners and Cleanup useEffect</a>

```jsx
import React from "react"

export default function WindowTracker() {
    
    const [windowWidth, setWindowWidth] = React.useState(window.innerWidth)
    
    React.useEffect(() => {

        // The 'watchWidth' function and the eventlistener statement doesn't necessarily need to be in the useEffect but it is better for cleanup purposes
        function watchWidth() {
            console.log("Setting up...")
            setWindowWidth(window.innerWidth)
        }

        // It doesn't matter about the dependencies in the 2nd arg of useEffect and the # of times this gets rendered but
        window.addEventListener("resize", watchWidth)    // Everytime the window is resized, it calls watchWidth function

        // We always want to remove the eventListener by returning this cleanup function that calls removeEventListener
        return function() {
            console.log("Cleaning up...")
            window.removeEventListener("resize", watchWidth)
        }
    }, [])
    
    return (
        // As you resize the window, the window width gets displayed here in real-time
        <h1>Window width: {windowWidth}</h1>
    )
}
```

<h3 style="color:#fc0303">Conditional Rendering</h3>

> - <a style="color:#000000">How would you make an html element appear only when the value of a particular variable is true?</a>

```jsx
import React from "react";
import ReactDOM from "react-dom/client";

function Welcome() {
  let show = true;

  // The h1 tag wouldn't be displayed if show is false
  return (
    <>
      {show && <h1>Hi! I'm Kannika</h1>}
    </>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Welcome />);
```

<h3 style="color:#fc0303">CSS in React</h3>

> - <a style="color:#000000">For setting css in html, we use a string like style="...", in react what is used instead?</a>
>
> - <a style="color:#000000">What is the difference in convention for a css attribute in html vs in react?</a>
> - <a style="color:#000000">For ex: In html, style="background-color:blue;" , how would you do this in react?</a>

```jsx
import React from "react";
import ReactDOM from "react-dom/client";

function Welcome() {
  // unlike css attributes in html, in React JS => Use camelCase for CSS property names
  let design = {
    color: "#ffffff",
    backgroundColor: "#cccccc"
  };

  // style={{}} outer-curly-brackets is to "go-into" javascript, inner-curly-brackets is to provide JS object of attributes
  return (
    <>
      <h1 style={design} className="title">Hi! I'm Kannika</h1>
    </>
  );
  // you can also give className (in camelCase) and provide the design like normal in .css file
  // in html, it would've been class="title"
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Welcome />);
```

<h3 style="color:#fc0303">Passing values to Child Components</h3>

> - <a style="color:#000000">How do you pass a value to a child component and how will the child component receive it?</a>

```jsx
import React from "react"

export default function App() {
    const [count, setCount] = React.useState(0)
    
    function add() {
        setCount(prevCount => prevCount + 1)
    }
    
    function subtract() {
        setCount(prevCount => prevCount - 1)
    }

    // you can pass in values to a child component like function args (which are actually accessed like objects)
    // state values and state-setter-functions can also be passed into child components, which will execute & update in real-time
    function Count(props){
        return (
            <div>
                <button className="counter--minus" onClick={props.decr}>–</button>
                <div className="counter--count">
                    <h1>{props.number}</h1>
                </div>
                <button className="counter--plus" onClick={props.incr}>+</button>
            </div>      
        )
    }
    // the above function can also be placed in a different file for organization

    return (
        <div className="counter">
            <Count number={count} decr={subtract} incr={add}/>
        </div>
    )
}
```

<h3 style="color:#fc0303">Handling Forms in React</h3>

> - <a style="color:#000000"></a>

```jsx
import React from "react"

export default function Form() {
    const [formData, setFormData] = React.useState(
        {
            firstName: "", 
            lastName: "", 
            email: "", 
            comments: "", 
            isFriendly: true,
            employment: "",
            favColor: ""
        }
    )

    // Only one handleChange function is needed to handle any change of a field in the form and store the updated input into formData state object
    function handleChange(event) {
        // event.target is the object and we are destructuring it
        const {name, value, type, checked} = event.target
        setFormData(prevFormData => {
            return {
                ...prevFormData,
                [name]: type === "checkbox" ? checked : value
            }
        })
    }
    
    function handleSubmit(event) {
        event.preventDefault()
        // submitToApi(formData)
        console.log(formData)
    }

    // onChange calls the function everytime we type on the input field,
    // and the handleChange updates the specific form object and
    // the value field uses the form object's value that we just stored to display it back into the text field

    // The name field must match with one of our object's key so that we can handle it easier in the handleChange function
    return (
        <form onSubmit={handleSubmit}>
            <input
                type="text"
                placeholder="First Name"
                onChange={handleChange}
                name="firstName"
                value={formData.firstName}
            />
            <input
                type="text"
                placeholder="Last Name"
                onChange={handleChange}
                name="lastName"
                value={formData.lastName}
            />
            <input
                type="email"
                placeholder="Email"
                onChange={handleChange}
                name="email"
                value={formData.email}
            />
            <textarea 
                value={formData.comments}
                placeholder="Comments"
                onChange={handleChange}
                name="comments"
            />
            <input 
                type="checkbox" 
                id="isFriendly" 
                checked={formData.isFriendly}
                onChange={handleChange}
                name="isFriendly"
            />
            { // htmlFor is to indicate which input field its associated to (in this case, it is a label for the checkbox because it matches the id and htmlFor) }
            <label htmlFor="isFriendly">Are you friendly?</label>
            <br />
            <br />
            
            <fieldset>
                <legend>Current employment status</legend>
                { // for radio buttons, we manually send in the value instead of fetching it from formData object
                  // however, the boolean value for checked is set based on the respective formData object
                  // 'name' is employment which matches the key in our formData object }
                <input 
                    type="radio"
                    id="unemployed"
                    name="employment"
                    value="unemployed"
                    checked={formData.employment === "unemployed"}
                    onChange={handleChange}
                />
                <label htmlFor="unemployed">Unemployed</label>
                <br />
                
                <input 
                    type="radio"
                    id="part-time"
                    name="employment"
                    value="part-time"
                    checked={formData.employment === "part-time"}
                    onChange={handleChange}
                />
                <label htmlFor="part-time">Part-time</label>
                <br />
                
                <input 
                    type="radio"
                    id="full-time"
                    name="employment"
                    value="full-time"
                    checked={formData.employment === "full-time"}
                    onChange={handleChange}
                />
                <label htmlFor="full-time">Full-time</label>
                <br />
            </fieldset>
            <br />
            
            <label htmlFor="favColor">What is your favorite color?</label>
            <br />
            { // dropdown option works like this }
            <select 
                id="favColor" 
                value={formData.favColor}
                onChange={handleChange}
                name="favColor"
            >
                <option value="red">Red</option>
                <option value="orange">Orange</option>
                <option value="yellow">Yellow</option>
                <option value="green">Green</option>
                <option value="blue">Blue</option>
                <option value="indigo">Indigo</option>
                <option value="violet">Violet</option>
            </select>
            <br />
            <br />
            <button>Submit</button>
        </form>
    )
}
```
