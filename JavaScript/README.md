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

<h3 style="color:#fcc603">Arrays</h3>

```javascript
arr = Array.from(mySet);    // set to array

arr.sort(function(a, b) {return a-b;});    // built-in sort

arr.push(9);    // append number 9 to arr

arr1.concat(arr2)    // arr1+arr2 returns concatenation of 2 arrays

Array.from(mySet);    // returns an array from set

arr.slice(0, i);    // return arr[0:i]

arr = str.split("");    // returns array of char from str

arr.reduce((partialSum, a) => partialSum + a, 0);    // returns the sum of all elements in the array

Math.max(...arr);    // returns the max element of the array

arr.reverse();   
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

/* Constructor */
function Person(firstName, lastName, age, eyeColor) {
  this.firstName = firstName; 
  this.lastName = lastName;
  this.age = age;
  this.eyeColor = eyeColor;
  this.changeAge = function (age) {
    this.age = age;
  };
}

const fighter1 = new Person("Nina", "Williams", 24, "blue");    // using the constructor
const fighter2 = new Person("Jin", "Kazama", 21, "grey");
```
