

# JavaScript Technical Paper

## Different Data Types in JavaScript

JavaScript has **two types of data types**:

### Primitive Types

* string
* number
* boolean
* undefined
* null
* bigint
* symbol

```js
let name = "Abhi";     // string
let age = 22;         // number
let isStudent = true; // boolean
let x;                // undefined
let y = null;         // null
```

### Non-Primitive (Reference Types)

* object
* array
* function

```js
let person = { name: "Abhi", age: 22 }; // object
let arr = [1, 2, 3];                   // array
function greet() {}                    // function
```

---

## Scopes in JavaScript

Scope means **where a variable can be used**.

### Global Scope

Accessible everywhere.

```js
let a = 10;

function test() {
  console.log(a); // works
}
```

### Function Scope

Accessible only inside function.

```js
function test() {
  let b = 20;
  console.log(b);
}

// console.log(b); error
```

###  Block Scope

Inside `{}` (only for let & const).

```js
if (true) {
  let c = 30;
  console.log(c);
}

// console.log(c); error
```

---

## let, var, const

###  var

* function scoped
* can redeclare
* hoisted

```js
var a = 10;
var a = 20; // allowed
```

### let

* block scoped
* cannot redeclare

```js
let a = 10;
// let a = 20;  error
```

### const

* block scoped
* cannot reassign

```js
const a = 10;
// a = 20; error
```

---

## Why We Must Not Use `var`

Problems with `var`:



###  Redeclaration allowed

```js
var a = 10;
var a = 20; // confusion
```

### Hoisting issues

```js
console.log(a); // undefined
var a = 10;
```

So always use **let or const**.

---

## Why Using Global Variables is Bad

###  Problem : Name conflict

```js
let a = 10;

function test() {
  let a = 20;
}
```

###  Problem : Hard to debug

Anyone can change it.

```js
let count = 0;

function update() {
  count++;
}
```

### Problem : Memory stays forever

 Use local variables instead.

---

## Truthy and Falsy Values

###  Falsy values (only these are false):

* false
* 0
* "" (empty string)
* null
* undefined
* NaN

```js
if (0) {
  console.log("hello");
} else {
  console.log("false"); // runs
}
```

###  Truthy values

Everything else is true.

```js
if ("hi") {
  console.log("true"); // runs
}
```

---

## Function Hoisting

Functions can be used **before declaration**.

```js
greet();

function greet() {
  console.log("Hello");
}
```

 This works because of **hoisting**.

---

## What Happens if Function Has No Return

If no return → it returns **undefined**.

```js
function test() {
  console.log("Hello");
}

let result = test();
console.log(result); // undefined
```

---

## Different Ways of Declaring Functions

### Function Declaration

Can call before definition.

```js
function add(a, b) {
  return a + b;
}
```

---

### Function Expression

Stored in variable.

```js
const add = function(a, b) {
  return a + b;
};
```

---

### Arrow Function

Short syntax.

```js
const add = (a, b) => a + b;
```

---

###  Anonymous Function

No name.

```js
setTimeout(function() {
  console.log("Hello");
}, 1000);
```

---

###  IIFE (Immediately Invoked Function)

Runs immediately.

```js
(function() {
  console.log("Run instantly");
})();
```

---





## Pass by Value (using function)

Primitive values are copied when passed to function.

```js
function changeValue(x) {
  x = 20;
  console.log("Inside function:", x);
}

let a = 10;

changeValue(a);

console.log("Outside function:", a);
```

Output:

```
Inside function: 20
Outside function: 10
```

Why:

* Function gets a **copy**
* Original value does not change

---

## Pass by Reference (using function)

Objects are passed by reference (actually reference value is copied).

```js
function changeObject(obj) {
  obj.name = "Amit";
  console.log("Inside function:", obj);
}

let person = { name: "Ravi" };

changeObject(person);

console.log("Outside function:", person);
```

Output:

```
Inside function: { name: "Amit" }
Outside function: { name: "Amit" }
```

Why:

* Function gets reference to same object
* So original object changes


---

## Different Types of Loops

### for loop (numbers)

Used when count is known.

```js
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

---

### for...in

Used for object keys.

```js
let obj = { a: 1, b: 2 };

for (let key in obj) {
  console.log(key, obj[key]);
}
```

---

### for...of

Used for arrays or iterable.

```js
let arr = [10, 20, 30];

for (let value of arr) {
  console.log(value);
}
```

---

### forEach

Used for arrays.

```js
let arr = [1, 2, 3];

arr.forEach((item) => {
  console.log(item);
});
```

Why: cleaner than loop.

---

### while loop

Used when condition based.

```js
let i = 0;

while (i < 3) {
  console.log(i);
  i++;
}
```

---



##  Popular Array Utility Methods

---


### Array.pop (mutable)

Removes last item.

```js
let arr = [1, 2, 3];
arr.pop();

console.log(arr); // [1, 2]
```

---

### Array.push (mutable)

Adds item at end.

```js
let arr = [1, 2];
arr.push(3);

console.log(arr); // [1, 2, 3]
```

---

### Array.concat (immutable)

Merges arrays.

```js
let a = [1, 2];
let b = [3, 4];

let result = a.concat(b);
console.log(result); // [1,2,3,4]
```

---

### Array.slice (immutable)

Returns part of array.

```js
let arr = [1, 2, 3, 4];

let result = arr.slice(1, 3);
console.log(result); // [2,3]
```

---

### Array.splice (mutable)

Add/remove elements.

```js
let arr = [1, 2, 3];

arr.splice(1, 1); // remove 1 item
console.log(arr); // [1,3]
```

---

### Array.join (immutable)

Convert array to string.

```js
let arr = ["a", "b", "c"];

let str = arr.join("-");
console.log(str); // a-b-c
```

---

### Array.flat (immutable)

Flattens nested arrays.

```js
let arr = [1, [2, [3]]];

let result = arr.flat(2);
console.log(result); // [1,2,3]
```

---

## Finding Methods

### Array.find

Returns first match.

```js
let arr = [1, 2, 3];

let result = arr.find(x => x > 1);
console.log(result); // 2
```

---

### Array.indexOf

Returns index.

```js
let arr = [10, 20, 30];

console.log(arr.indexOf(20)); // 1
```

---

### Array.includes

Checks presence.

```js
let arr = [1, 2, 3];

console.log(arr.includes(2)); // true
```

---

### Array.findIndex

Returns index of match.

```js
let arr = [5, 10, 15];

let index = arr.findIndex(x => x > 9);
console.log(index); // 1
```

---

## Higher Order Functions

These take function as input.

---

### Array.forEach (mutable behaviour)

Loops array.

```js
let arr = [1, 2];

arr.forEach(x => console.log(x));
```

Where: simple iteration.

---

### Array.filter (immutable)

Filters data.

```js
let arr = [1, 2, 3, 4];

let result = arr.filter(x => x > 2);
console.log(result); // [3,4]
```

Why: remove unwanted data.

---

### Array.map (immutable)

Transforms data.

```js
let arr = [1, 2, 3];

let result = arr.map(x => x * 2);
console.log(result); // [2,4,6]
```



---

### Array.reduce (immutable)

Reduces to single value.

```js
let arr = [1, 2, 3];

let sum = arr.reduce((acc, curr) => acc + curr, 0);
console.log(sum); // 6
```

Why: sum, total, calculations.

---

### Array.sort (mutable)

Sorts array.

```js
let arr = [3, 1, 2];

arr.sort();
console.log(arr); // [1,2,3]
```

Note: modifies original.

---


## Array Method Chaining

Using multiple methods together.

```js
let arr = [1, 2, 3, 4, 5];

let result = arr
  .filter(x => x > 2)
  .map(x => x * 2)
  .reduce((a, b) => a + b, 0);

console.log(result); // 24
```

Why:

* Clean code
* Less variables
* Easy to read

Where:
Used in real projects, React, APIs.

---







## Popular String Utility Methods

Strings are **immutable** (original string does not change)

### toUpperCase

```js
let str = "hello";
let result = str.toUpperCase();

console.log(result); // HELLO
```

---

### toLowerCase

```js
let str = "HELLO";
console.log(str.toLowerCase()); // hello
```

---

### includes

```js
let str = "javascript";

console.log(str.includes("script")); // true
```

---

### slice

```js
let str = "javascript";

console.log(str.slice(0, 4)); // java
```

---

### replace

```js
let str = "hello world";

console.log(str.replace("world", "JS")); // hello JS
```

---

### trim

```js
let str = "  hi  ";

console.log(str.trim()); // "hi"
```

Why: remove spaces

---

## Popular Object Utility Methods

Objects are **mutable**

---

### Object.keys (immutable)

```js
let obj = { a: 1, b: 2 };

console.log(Object.keys(obj)); // ["a","b"]
```

---

### Object.values (immutable)

```js
console.log(Object.values(obj)); // [1,2]
```

---

### Object.entries (immutable)

```js
console.log(Object.entries(obj));
// [["a",1],["b",2]]
```

---

### Object.assign (mutable target)

```js
let a = { x: 1 };
let b = { y: 2 };

Object.assign(a, b);

console.log(a); // {x:1, y:2}
```

---

### Spread with object (immutable)

```js
let obj1 = { a: 1 };
let obj2 = { ...obj1, b: 2 };

console.log(obj2);
```

---



### forEach

Use when no return needed

```js
[1,2,3].forEach(x => console.log(x));
```

---

### map

Use when transforming data

```js
let result = [1,2,3].map(x => x * 2);
```

---

### filter

Use when selecting data

```js
let result = [1,2,3,4].filter(x => x > 2);
```

---

### reduce

Use when single value needed

```js
let sum = [1,2,3].reduce((a,b) => a + b, 0);
```

---

## Immutable and Mutable Methods

### Mutable (change original)

* push
* pop
* splice
* sort

```js
let arr = [3,1,2];
arr.sort();

console.log(arr); // changed
```

---

### Immutable (do not change original)

* map
* filter
* slice
* concat

```js
let arr = [1,2,3];

let newArr = arr.map(x => x * 2);
```

---

## Error Handling (try...catch)

Used to handle runtime errors

```js
try {
  let x = y; // error
} catch (err) {
  console.log("Error:", err.message);
}
```

Why:

* Prevent app crash
* Handle safely

---

## Throwing Errors

You can create your own error

```js
function checkAge(age) {
  if (age < 18) {
    throw new Error("Age is less than 18");
  }
}

checkAge(15);
```

---

## Difference: Error Object vs String

### Using Error object 

```js
throw new Error("Something went wrong");
```

### Using string 

```js
throw "Something went wrong";
```

Why Error object:

* Gives stack trace
* Better debugging

---

## Importance of catch Block

```js
try {
  JSON.parse("wrong");
} catch (err) {
  console.log("Handled error");
}
```

Why:

* Without catch → app crash
* With catch → safe handling

---

## Spread Operator

Used to copy or expand

```js
let arr = [1,2];
let newArr = [...arr, 3];

console.log(newArr);
```

---

## Template Literals

Use backticks ``

```js
let name = "Ravi";

console.log(`Hello ${name}`);
```

Why:

* Easy string formatting

---

## Default Parameters

```js
function greet(name = "Guest") {
  console.log(name);
}

greet(); // Guest
```

---

## Destructuring

Extract values easily

### Array destructuring

```js
let arr = [1,2];

let [a,b] = arr;

console.log(a, b);
```

---

### Object destructuring

```js
let obj = { name: "Ravi", age: 25 };

let { name, age } = obj;

console.log(name, age);
```

Why:

* Clean code
* Less typing

---





## Closures

Closure means function remembers outer variables.

```js id="q8d4z2"
function outer() {
  let count = 0;

  function inner() {
    count++;
    console.log(count);
  }

  return inner;
}

let fn = outer();

fn(); // 1
fn(); // 2
```

Why:

* Data privacy
* State maintain

Where:

* Counters, caching

---

## Difference Between Arrow and Regular Functions

### Regular Function

```js id="u8j2vx"
function test() {
  console.log(this);
}
```

### Arrow Function

```js id="b3g7pq"
const test = () => {
  console.log(this);
};
```

Key Differences:

* Arrow has no own `this`
* Regular has its own `this`
* Arrow is shorter

---

## Difference Between === and ==

### ==

Loose comparison (type conversion)

```js id="l2p6ok"
console.log(5 == "5"); // true
```

---

### ===

Strict comparison (no conversion)

```js id="5td7y2"
console.log(5 === "5"); // false
```

Why:
Always use `===` to avoid bugs

---

## Why value === undefined is Better than !value

### Problem with !value

```js id="w0qf8f"
let value = 0;

if (!value) {
  console.log("runs"); // wrong
}
```

---

### Correct way

```js id="g1k3sh"
if (value === undefined) {
  console.log("only undefined");
}
```

Why:
`!value` also matches:

* 0
* ""
* false
* null

---

## Array Utility Methods Chaining

Use multiple methods together.

```js id="7h5m2x"
let arr = [1,2,3,4];

let result = arr
  .filter(x => x > 1)
  .map(x => x * 2);

console.log(result); // [4,6,8]
```

Why:

* Clean code
* Less variables

---

## Difference Between null and undefined

### undefined

```js id="5k2d1p"
let a;
console.log(a); // undefined
```

---

### null

```js id="c7f9zn"
let b = null;
```

Difference:

* undefined → not assigned
* null → intentionally empty

---

## Import and Export 

### Export

```js id="p9r2dw"
// math.js
function add(a, b) {
  return a + b;
}

module.exports = add;
```

---

### Import

```js id="k4x8js"
// app.js
const add = require("./math");

console.log(add(2,3));
```

Why:

* Code reuse
* Modular code

---

## Console Methods

### console.log

```js id="ffj9o7"
console.log("Hello");
```

---

### console.error

```js id="z6k4dw"
console.error("Error happened");
```

---

### console.info

```js id="2o1n7y"
console.info("Info message");
```

---

### console.warn

```js id="6l2v8x"
console.warn("Warning");
```

---

### console.table

```js id="8d1c3w"
console.table([{a:1},{a:2}]);
```

Why:

* Debugging
* Better logs

---



### Variable Naming

```js id="j2w8y4"
let userName = "Ravi"; // good
let x = "Ravi";        // bad
```

---

### Loop Naming

```js id="l9v2q7"
for (let i = 0; i < 5; i++) {}
```

---

### Use const by default

```js id="a1c5e8"
const pi = 3.14;
```

---




## Named vs Anonymous Functions

### Named Function

```js id="p7k2v9"
function add(a, b) {
  return a + b;
}
```

---

### Anonymous Function

```js id="d3w8q1"
const add = function(a, b) {
  return a + b;
};
```

Difference:

* Named → reusable, better debugging
* Anonymous → used inline

---

## Variable Number of Arguments

Using rest operator

```js id="y6t9m3"
function sum(...nums) {
  return nums.reduce((a,b) => a + b, 0);
}

console.log(sum(1,2,3)); // 6
```

Why:

* Flexible inputs

---





## Debugging Strategies

Debugging means finding and fixing errors.

---




### Use debugger keyword

```js id="g5t8zn"
let a = 5;
debugger;
let b = a * 2;
```

Why:

* Stops code in browser dev tools
* Inspect variables






---

### Check Types

```js id="s2n8qw"
let x = "10";

console.log(typeof x); // string
```

Why:

* Avoid type bugs

---



### Use try...catch

```js id="q8w2pl"
try {
  JSON.parse("wrong");
} catch (e) {
  console.log(e.message);
}
```

---






