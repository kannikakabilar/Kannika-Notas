<h1 style="color:#fcc603">JavaScript</h1>

JavaScript's \<script> tag should be placed before the closing \<body> tag to reduce page loading time.

<h3 style="color:#fcc603">Variables</h3>

- Variables declared without a keyword become **global variables**, irrespective of where they are declared (ie: in a function)
- Variables declared with **let** & **const**
    - must be declared before use
    - cannot be redeclared
    - can only be used within block scope that it was declared
    - cannot bind with this (for objects)
    - cannot be hoisted

\* **let** allows to change values of variables while **const** <span style="color:red">does not</span>!

- **var** is used for supporting old browsers, allows hoisting, and binds to this

\* **Hoisting** is JavaScript's default behavior of moving all declarations (not initialization) to the top of the current scope
(var variables can be used first and then declared after)

```javascript
myGlobalVar = 9;    // variable w/o keyword => global variable
var count = 99;
var count;        // can be re-declared and it would still have value 99
let count = 0;
const count = 0;    // const won't allow you to change its value
console.log("hello kan");    // print

var myFuncName = function(p1, p2) {
    ...
}
```

<h3 style="color:#fcc603">Strings</h3>

```javascript
for(let i=0; i<{arr/str}.length; i++){
    if({arr/str}[i] == ...){
        ...
    }
}

str1.localeCompare(str2)==0     // returns true if both strs are exactly equal

parseInt("1999");    // returns 1999 Number

num.toString();    // returns number stored in num to a string

let str = arr.join('');    // combine elements of arr with empty string and return string
```

- Get parts of a string/Array: **slice(start, end)**

<h3 style="color:#fcc603">Arrays</h3>

```javascript
arr = Array.from(mySet);    // set to array

arr.sort(function(a, b) {return a-b;});    // by default js sorts as strings to sort numbers input this function

arr.push(9);    // append number 9 to arr

arr1.concat(arr2)    // arr1+arr2 returns concatenation of 2 arrays

arr.slice(0, i);    // return arr[0:i]

arr = str.split("");    // returns array of char from str

arr.reduce((partialSum, a) => partialSum + a, 0);    // returns the sum of all elements in the array

Math.max(...arr);    // returns the max element of the array

arr.reverse();

const planets = ["Mercury", "Venus", "Neptune"];
planets[6] = "Jupiter";  // Creates undefined "holes" in planets

const fruits = ["Banana", "Orange", "Apple", "Mango"];
let fruit = fruits.pop();    // removes and returns the last element | fruit = Mango
let fruit = fruits.shift();    // removes and returns the first element | fruit = Banana
fruits.unshift("Lemon");    // adds new element to the beginning of the array and returns array length

const fruits = ["Banana", "Orange", "Apple", "Mango"];
/* new elements are added at index 2, 2 elements from index 2 and 3 are removed and returned from og array, "Lemon" and "Kiwi" are  the new elements added to the array */
let removed = fruits.splice(2, 2, "Lemon", "Kiwi");

fruits.includes("Mango"); // is true

/* Filtering an array */
const numbers = [45, 4, 9, 16, 25];
const over18 = numbers.filter(myFunction);
function myFunction(value, index, array) {
  return value > 18;
}
```

<h3 style="color:#fcc603">Hash Sets</h3>

```javascript
let mySet = new Set();

let mySet = new Set(arr);    // array to set

mySet.has(num);    // returns true if the set contains num

mySet.add(new_num);   // add new_num to set

mySet.size    // return size of set

mySet.delete(0);    // delete zero from set

```

<h3 style="color:#fcc603">Hash Maps</h3>

```javascript
let freq = new Map();    // freq = {}; also works
freq.has(num);
freq.set(arr[i], freq.get(arr[i])+1);

for(let [key, value] of freq){    // loop through keys and values of map
    if(key == .. && value == ...) ...
}

for(let key in freq){    // loop through key of map
    if(freq[key] == ...) { ... }
}
```

<h3 style="color:#fcc603">Checking Equality in JS</h3>

```javascript
// Check if any 2 javascript objects are equal
const equalsCheck = (a, b) => {
    return JSON.stringify(a) === JSON.stringify(b);
}

if(equalsCheck(arr1, arr2)){
    return true;    // return true if arr1 and arr2 are equal
}else{
    return false;
}
```

<h3 style="color:#fcc603">Functions</h3>

```javascript
// Anonymous Self-Invoking Function
(function () {
  let x = "Hello!!";  // I will invoke myself
})();

// Creating a function using a Function constructor
const sum = new Function('a', 'b', 'return a + b');
console.log(sum(2, 7));    // Expected output: 9

// With call(), an object can use a method belonging to another object.
const person = {
  fullName: function(city, country) {
    return this.firstName + " " + this.lastName + "," + city + "," + country;
  }
}
const person1 = {
  firstName:"Kannika",
  lastName: "Kabilar"
}
person.fullName.call(person1, "Toronto", "Canada");
// Same as call() but => The apply() method takes args an array instead of separately
person.fullName.apply(person1, ["Toronto", "Canada"]);

/* Closure */
const add = (function () {
  let counter = 0;
  return function () {counter += 1; return counter}
})();    // Calls itself and returns a function which is stored in add - this allows the function to have 'counter' as a private variable

add();
add();
add();
// the counter is now 3  
```

**Arguments are Passed by Value** and **Objects are Passed by Reference**

<h3 style="color:#fcc603">Objects</h3>

```javascript
// Creating an object
const person = {
  firstName: "Kannika",
  lastName : "Kabilar",
  id       : 1999,
  fullName : function() {
    return this.firstName + " " + this.lastName;
  }
};

// Accessing properties of an object
objectName.property      // person.age
objectName["property"]   // person["age"]
objectName[expression]   // x = "age"; person[x]

// Methods of an object
name = person.fullName();    
name = person.fullName;    // If you access the fullName property, without (), it will return the function definition

// JSON Stringify an object
const person = {
  name: "Kannika",
  age: 23,
  city: "Toronto"
};

let myString = JSON.stringify(person);
document.getElementById("demo").innerHTML = myString;   
// The result will be a string following the JSON notation: {"name":"Kannika", "age":23, "city":"Toronto"}
```

<h3 style="color:#fcc603">Regex</h3>

```javascript
let text = "Visit Canada!";
let n = text.search("Canada");    // n = 6
let result = text.replace(/canada/i, "USA");    // Search for 'canada' (case insensitive) and replace it; result = "Visit USA!"
```

<h3 style="color:#fcc603">Strict Mode</h3>

```javascript
x = 3.14;       // This will not cause an error
myFunction();

"use strict";
let x = 3.14;
delete x;    // This will cause an error because deleting is not allowed
```

<h3 style="color:#fcc603">Modules: Imports & Exports</h3>

```javascript
// Example 1
/* person.js */
export const name = "Kazuya";
export const age = 48;

/* main.js */    // Importing Named Exports
import { name, age } from "./person.js";

// Example 2
/* message.js */
const message = () => {
const name = "Jesse";
const age = 40;
return name + ' is ' + age + 'years old.';
};
export default message;

/* main.js */
import message from "./message.js";
```

<h3 style="color:#fcc603">Debugger</h3>

The debugger keyword stops the execution of JavaScript, and calls (if available) the debugging function.
With the debugger turned on, this code will stop executing before it executes the third line.

```javascript
let x = 15 * 5;
debugger;
document.getElementById("demo").innerHTML = x;
```

<h3 style="color:#fcc603">Objects vs. Classes</h3>
- Objects are used for creating a single entity with their own state & behaviour (almost like a specific instance of a class with its own unique property values)
- Classes are like a blueprint of an object that allows to create multiple instances (multiple objects with same state and behaviour)

<h3 style="color:#fcc603">Classes</h3>

```javascript
class Person {    // Every class must have a method called constructor
  constructor(name, birthYear) {
    this.name = name;
    this.birthYear = birthYear;
  }
  age(currentYear) {    // methods don't need function keyword
    return currentYear - this.year;
  }
}
-
class Student extends Person {     // use extends to inherit from parent class like java
  static counter = 0;    // Static property (used from class not from any instance of class)
  constructor(name, birthYear, id) {
    Student.counter += 1
    super(name, birthYear);    // methods and properties/attributes from parent method can be used in this class
    this.id = id;
  }
  info() {
    let year = new Date();    // * classes follow strict mode rules
    return 'Name: ' + this.name + ', age: ' + this.age(year) + ', student ID: ' + this.id;
  }
-
// Getters and Setters
  get sname() {    // even if the getter is a method, you don't use parentheses when you want to get the property value
    return this.name;
  }
  set sname(x) {
    this.name = x;
  }
}
-
// Static method - defined on the class itself. Cannot call a static method on an object, only on an object class.
static getTotal() {
    return "Total Students: " + Student.counter;
  }


let year = date.getFullYear();

let kan = new Person("Kannika", 2023);
document.getElementById("demo").innerHTML=​ "Hi, I am " + kan.age(year) + " years old.";
document.getElementById("demo2").innerHTML=​ Student.getTotal();
```

<h3 style="color:#fcc603">JSON</h3>

Stores objects as text

**JSON.parse()**    -    converts JSON strings into JavaScript objects

**JSON.stringify()**    -    converts an object into a JSON string

\* JSON values cannot be: function, date, undefined ; but it can be string, number, object, array ...

```javascript
<p id="demo"></p>
<script>
// jsonText contains a string of how objects are stored in JSON.stringify(obj1) is called
// object employees is an array and it contains 3 person object
let jsonText = '{"employees":[' +
'{"firstName":"Steve","lastName":"Fox" },' +
'{"firstName":"Anna","lastName":"Williams" },' +
'{"firstName":"Julia","lastName":"Chang" }]}';

const obj = JSON.parse(jsonText);    // Convert the json formatted string into a JavaScript object
document.getElementById("demo").innerHTML =
obj.employees[1].firstName + " " + obj.employees[1].lastName;
</script>
```
