<h1 style="color:#fcc603">JavaScript</h1>

<h3 style="color:#fcc603">Intro</h3>

> - <a style="color:#000000">Why should JS's \<script> tag be placed at the end before the closing \<body> tag instead of the start?</a>
>
> - <a style="color:#000000">What are the 4 ways to declare a variable in JS?</a>
>
> - <a style="color:#000000">What is the main difference between let and const?</a>
>
> - <a style="color:#000000">What is Hoisting?</a>
> <br> **Hoisting** is JavaScript's default behavior of moving all declarations (not initialization) to the top of the current scope
(var variables can be used first and then declared after)
>


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

> - <a style="color:#000000">Is a string created with double quotes or single quotes?</a>
>
> - <a style="color:#000000">Are strings mutable or immutable in JS and what happens when you modify an already created string?</a>
>
> - <a style="color:#000000">How would you loop through the characters of a String and access a character at the specific index in JS?</a>
>
> - <a style="color:#000000">How do you compare two strings?</a>
>
> - <a style="color:#000000">How do you change a String into a Number in JS?</a>
> - <a style="color:#000000">How do you change a Number into a String and how do you change it into a binary string?</a>
>
> - <a style="color:#000000">How do you replace all occurence of a particular string with another string or an empty string?</a>
>
> - <a style="color:#000000">How can you convert and merge array elements into a string?</a>
>
> - <a style="color:#000000">How can you format a string to embed code variables?</a>
>
> - <a style="color:#000000">What is returned when you execute the following statement: i\) Number('    -12.34    ');  ii\) Number(1,2);</a>
>
> - <a style="color:#000000">Notable string functions: toUpperCase, trim, includes, startsWith, endsWith, slice</a>

```javascript
for(let i=0; i<{arr/str}.length; i++){
    if({arr/str}[i] == ...){
        ...
    }
}

str1 === str2                                              // returns true if both strings are equal
str1 < str2                                                // returns true if str1 comes before str2 in a dictionary
str1.localeCompare(str2)==-1                               // returns true if str1 before str2 and returns 1 for vice versa and 0 if equal

parseInt("1999");                                          // returns 1999 Number

num.toString();                                            // returns number stored in num to a string
num.toString(2);                                           // returns number stored in num to a binary string

str.replaceAll("Canada", "USA");                           // replace all instances of "Canada" with "USA" in str
str.replaceAll("c", "");                                   // removes all instances of c in str

let str = arr.join('');                                    // combine elements of arr with empty string and return string

let grade = 99;
console.log(`You have ${grade > 90 ? 'passed' : 'failed'} the exam.`);

Number('    -12.34    ');                                  // returns -12.34 from trimming begining and ending white spaces
Number('1,2');                                             // returns NaN (Not a Number)

let text = "Hello World!";
let result = text.toUpperCase();                           // "HELLO WORLD!"

let text = "       Hello World!        ";
let result = text.trim();                                  // "Hello World!"

let text = "Hello world, welcome to the universe.";
let result = text.includes("world");                       // true
text.startsWith("Hello");                                  // true
text.endsWith("universe.");                                // true

let text = "Hello world!";
let result1 = text.slice(0, 5);                            // from position 0 to 5
let result2 = text.slice(3)                                // from position 3 to end
```

- Get parts of a string/Array: **slice(start, end)**

<h3 style="color:#fcc603">Arrays</h3>

> - <a style="color:#000000">How do you convert a set to an array?</a>
>
> - <a style="color:#000000">How do you get the maximum element of an array?</a>
>
> - <a style="color:#000000">How do you get the length of the arguments passed when it is defined like this? function(...args) { ... }</a>
>
> - <a style="color:#000000">If an array has 3 elements, what gets returned when you access its 6th element?</a>
>
> *Note: The following functions modify the original array
> - <a style="color:#000000">How do you use the built-in function sort to sort an array of Numbers?</a>
>
> - <a style="color:#000000">What do these following functions do?
> 	- i\) arr.shift();
>  	- ii\) arr.pop();
> 	- iii\) arr.unshift(9);
> 	- iv\) fruits.splice(2, 2, "Lemon", "Kiwi");</a>
>
> --------------------------------------------------------------------------------------------
> 
> *Note: The following functions make changes and return a new array
> - <a style="color:#000000">How do you combine two different arrays into one?</a>
>
> - <a style="color:#000000">How does the filter function work?</a>
>
> - <a style="color:#000000">How does the map function work?</a>
> ---------------------------------------------------------------------------------------------
> - <a style="color:#000000">How do you use reduce to sum all elements in the array to get the total?</a>
>
> - <a style="color:#000000">How do you destructure an array to assign the values stored in the array to separate variables?</a>
>
> - <a style="color:#000000">Can arrays in JS store different data types?</a>
>
> - <a style="color:#000000">How do you get the index of a given element of an array?</a>
>
> - <a style="color:#000000">How do you check if an array contains a given element?</a>
>
> - <a style="color:#000000">How do these following functions work with an array?
> 	- i\) arr.every(...);
>  	- ii\) arr.some(...);
> 	- iii\) arr.find(...);
> 	- iv\) arr.findIndex(...);</a>
>
> - <a style="color:#000000">What is the difference between the rest operator and the spread operator?</a>

```javascript
arr = Array.from(mySet);    // set to array

arr.slice(0, i);    // return arr[0:i]
arr = str.split("");    // returns array of char from str
arr.reverse();

Math.max(...arr);    // returns the max element of the array

var argumentsLength = function(...args) {
	return [...args].length;    // return length of arguments passed to function - LeetCode Q2703
};

const planets = ["Mercury", "Venus", "Neptune"];
planets[6] = "Jupiter";  // Creates undefined "holes" in planets

arr.sort(function(a, b) {return a-b;});    // by default js sorts as strings to sort numbers input this function
arr.push(9);    // append number 9 to arr

const fruits = ["Banana", "Orange", "Apple", "Mango"];
let fruit = fruits.pop();    // removes and returns the last element | fruit = Mango
let fruit = fruits.shift();    // removes and returns the first element | fruit = Banana
fruits.unshift("Lemon");    // adds new element to the beginning of the array and returns array length

const fruits = ["Banana", "Orange", "Apple", "Mango"];
/* new elements are added at index 2, 2 elements from index 2 and 3 are removed and returned from og array, "Lemon" and "Kiwi" are  the new elements added to the array */
let removed = fruits.splice(2, 2, "Lemon", "Kiwi");

fruits.includes("Mango"); // is true

arr1.concat(arr2)    // arr1+arr2 returns concatenation of 2 arrays

/* Filtering an array */
const numbers = [45, 4, 9, 16, 25];
const over18 = numbers.filter(myFunction);
function myFunction(value, index, array) {
  return value > 18;
}

/* Mapping in an array */
let arr = [1, 2, 3, 4]
const newArr = arr.map((x) => x-1);    // newArr = [0, 1, 2, 3]

let total = arr.reduce((partialSum, a) => partialSum + a, 0);    // returns the sum of all elements in the array

const numOfMoons = [0, 2, 14];
const [venus, mars, neptune] = numOfMoons;
console.log(neptune);    // outputs 14

const nums = [1, 'two', 3, 'four'];
nums.indexOf('two');    // returns 1
nums.includes(1);       // returns true

const nums2 = [1, 3, 5, 7, 9];
nums2.every((n) => n%2 !== 0);    // returns true since every element passes the condition
nums2.some((n) => n%2 !== 0);    // returns true since some element passes the condition
nums2.find((n) => n>5);          // returns 7 (the first value that passes the condition)
nums2.findIndex((n) => n>9);     // returns -1 (same as above but returns the index)

// Rest operator appears on the left-side of the assignment operator and it can only be placed as the last element in the list
const [a, b, ...everythingElse] = [0, 1, 1, 2, 3, 5, 8];
everythingElse    // returns [1, 2, 3, 5, 8]

// Spread operator appears on the rigth-side of the assignment operator and it can appear anywhere & any # of times in the array
const oneToFive = [1, 2, 3, 4, 5];
const oneToTen = [...oneToFive, 6, 7, 8, 9, 10];
oneToTen    // returns [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
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

Stores JS objects or JS arrays as text

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

<h3 style="color:#fcc603">AJAX</h3>

- allows the feature of not collecting all data from server when loading the webpage only when it is requested

\* The below chunk of code can be put inside a function & the function can be executed when a button is clicked or when a letter is typed in an input field
```javascript
// Step 1: Create an instance of an XMLHttpRequest
var xhttp = new XMLHttpRequest();

// Step 2: Either we are receiving data from webserver (GET) or we are sending to webserver (POST)
xhttp.open('GET', 'some-url.com');
// The url should be a datafile in the following format: JSON, XML, PHP, ASP, Database

// Step 3: Execute this function when the webpage requests it
xhttp.onload = function() {
    . . .  // use xhttp.responseText or this.responseText to use the data that we collected from url
    . . .  // it contains contains JSON stringified data (or string data) or this.responseXML if url is xml file
};

// Step 4: Send either our 'GET' request or 'POST' request to webserver
xhttp.send();
// If 'POST': xhttp.send("fname=Kannika&lname=Kabilar");
```

<h3 style="color:#fcc603">jQuery</h3>

- It can be used for: animation, event handling, html element manipulation, and
    - traversing & filtering through html elems => useful for searching through text in webpage
- It can also be used with AJAX

```javascript
myElement = $("#id01");
// same as: myElement = document.getElementById("id01");

myElements = $("p");    // return all <p> elements
// same as: myElements = document.getElementsByTagName("p");

myElements = $("p.intro");   // return a list of all <p> elements with class="intro"
// same as: myElements = document.querySelectorAll("p.intro");
```

```html
<-- Filtering html elems with jQuery example -->
<!DOCTYPE html>
<html>
<head>
<-- include below line to use jQuery -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
<script>
$(document).ready(function(){
  $("#myInput").on("keyup", function() {
    var value = $(this).val().toLowerCase();
    $("#myList li").filter(function() {
      $(this).toggle($(this).text().toLowerCase().indexOf(value) > -1)
    });
  });
});
</script>
</head>
<body>

<h2>Filterable List</h2>
<p>Type something in the input field to search the list for specific items:</p>  
<input id="myInput" type="text" placeholder="Search...">
<br>

<ul id="myList">
  <li>First item</li>
  <li>Second item</li>
  <li>Third item</li>
  <li>Fourth</li>
</ul>
  
</body>
</html>
```


***Note**: getElementById is an example of HTML DOM
- HTML DOM can be used to change text of html elems, change its css, perform form validation, and animation.
