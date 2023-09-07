<h1 style="color:#fcc603">JavaScript</h1>

<h3 style="color:#fcc603">Variables</h3>

```javascript
var count = 0;
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
