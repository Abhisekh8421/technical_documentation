# JavaScript Execution and Asynchronous Concepts

## How JavaScript Executes Code

JavaScript is a single-threaded language, which means it can execute one task at a time. It uses a component called the Call Stack to manage execution. When a function is called, it is pushed onto the stack, and when it finishes, it is removed.

JavaScript execution happens in two main phases:

* Memory Creation Phase: Variables and functions are stored in memory.
* Execution Phase: Code runs line by line.

Example:

```javascript
function greet() {
  console.log("Hello");
}

greet();
console.log("World");
```

Execution:

* greet function is stored in memory
* greet() is called and pushed to stack → logs "Hello"
* removed from stack
* then "World" is logged

Output:
Hello
World

---

## Difference Between Synchronous and Asynchronous Code

Synchronous code executes line by line, waiting for each operation to complete before moving to the next.

Asynchronous code allows some operations to run in the background without blocking the execution of the rest of the code.

Example of synchronous:

```javascript
console.log("Start");
console.log("Middle");
console.log("End");
```

Output:
Start
Middle
End

Example of asynchronous:

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Async Task");
}, 2000);

console.log("End");
```

Output:
Start
End
Async Task

---

## Ways to Make Code Asynchronous

JavaScript provides several ways to handle asynchronous operations.

Callbacks
A function passed as an argument and executed later.

Example:

```javascript
function fetchData(callback) {
  setTimeout(() => {
    callback("Data received");
  }, 1000);
}

fetchData((data) => {
  console.log(data);
});
```

Promises
An object that represents a future value (resolved or rejected).

Example:

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Data loaded");
  }, 1000);
});

promise.then((data) => console.log(data));
```

Async/Await
A cleaner way to work with promises.

Example:

```javascript
async function getData() {
  const result = await promise;
  console.log(result);
}

getData();
```

---

## Web Browser APIs

Web Browser APIs are features provided by the browser to handle tasks like timers, DOM manipulation, and network requests. These APIs run outside the JavaScript engine.

Examples include:

* setTimeout
* DOM APIs
* fetch

Example:

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timer done");
}, 1000);

console.log("End");
```

Here, setTimeout is handled by the browser, not directly by JavaScript.

---

## Event Loop

The Event Loop is responsible for managing asynchronous behavior in JavaScript. It continuously checks if the Call Stack is empty. If it is, it takes tasks from the Callback Queue and pushes them to the Call Stack.

Flow:

* Code runs in Call Stack
* Async tasks go to Web APIs
* After completion, callbacks go to Queue
* Event Loop pushes them back to Call Stack

Example:

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Callback");
}, 0);

console.log("End");
```

Output:
Start
End
Callback

---

## What is Callback Hell

Callback Hell happens when multiple nested callbacks make the code hard to read and maintain.

Example:

```javascript
setTimeout(() => {
  console.log("Step 1");
  setTimeout(() => {
    console.log("Step 2");
    setTimeout(() => {
      console.log("Step 3");
    }, 1000);
  }, 1000);
}, 1000);
```

This structure becomes difficult to manage as it grows deeper.

---

## What is Inversion of Control in Callbacks

Inversion of Control means that you lose control over your code execution when you pass a callback to another function. You depend on that function to call your callback correctly.

Example:

```javascript
function doTask(callback) {
  callback();
}

doTask(() => {
  console.log("Task completed");
});
```

Here, you trust doTask to call your callback. If it fails or calls it incorrectly, your program may break.

---

# JavaScript Promises

## What is a Promise

A Promise is an object that represents the eventual completion or failure of an asynchronous operation. It acts like a placeholder for a value that will be available in the future.

Example:

```javascript
const promise = new Promise((resolve, reject) => {
  resolve("Success");
});

promise.then((data) => console.log(data));
```

---

## How to Create a New Promise

A Promise is created using the Promise constructor, which takes a function with resolve and reject.

Example:

```javascript
const promise = new Promise((resolve, reject) => {
  let success = true;

  if (success) {
    resolve("Data received");
  } else {
    reject("Error occurred");
  }
});
```

---

## States of a Promise

A Promise has three states:

Pending: Initial state
Fulfilled: Operation completed successfully
Rejected: Operation failed

Example:

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Done"), 1000);
});
```

---

## How to Consume a Promise

A Promise is consumed using .then and .catch.

Example:

```javascript
promise
  .then((data) => console.log(data))
  .catch((err) => console.log(err));
```

---

## Promise Chaining

Promise chaining allows you to execute multiple async operations in sequence.

---

## How to Chain Promises Using .then

Each .then returns a new promise, allowing chaining.

Example:

```javascript
Promise.resolve(1)
  .then((val) => val + 1)
  .then((val) => val + 1)
  .then((val) => console.log(val));
```

Output:
3

---

## How to Handle Errors Using .catch

.catch handles errors in the chain.

Example:

```javascript
Promise.reject("Error")
  .then((data) => console.log(data))
  .catch((err) => console.log(err));
```

---

## finally Block in a Promise Chain

.finally runs regardless of success or failure.

Example:

```javascript
Promise.resolve("Done")
  .then((data) => console.log(data))
  .finally(() => console.log("Cleanup"));
```

---

## What Happens When Error is Thrown Inside .then with .catch

The error is caught by the nearest .catch.

Example:

```javascript
Promise.resolve()
  .then(() => {
    throw new Error("Something went wrong");
  })
  .catch((err) => console.log(err.message));
```

---

## What Happens When Error is Thrown Inside .then Without .catch

The error becomes an unhandled promise rejection.

Example:

```javascript
Promise.resolve()
  .then(() => {
    throw new Error("Unhandled error");
  });
```

---

## Why .catch Should Be Placed at the End

Placing .catch at the end ensures it handles errors from all previous .then calls.

Example:

```javascript
Promise.resolve()
  .then(() => {
    throw new Error("Error in step 1");
  })
  .then(() => console.log("Step 2"))
  .catch((err) => console.log(err.message));
```

---

## Consuming Multiple Promises by Chaining

You can chain multiple async operations sequentially.

Example:

```javascript
Promise.resolve("Step 1")
  .then((data) => {
    console.log(data);
    return "Step 2";
  })
  .then((data) => {
    console.log(data);
    return "Step 3";
  })
  .then((data) => console.log(data));
```

---

## Using Promise.all

Runs multiple promises in parallel and resolves when all succeed.

Example:

```javascript
const p1 = Promise.resolve("A");
const p2 = Promise.resolve("B");

Promise.all([p1, p2]).then((results) => {
  console.log(results);
});
```

---

## Error Handling in Promises

Errors can be handled using .catch or try/catch with async/await.

Example:

```javascript
Promise.reject("Failed")
  .catch((err) => console.log(err));
```

---

## Why Error Handling is Important

Without proper error handling, failures can go unnoticed and break application flow.

Example:

```javascript
fetch("invalid-url")
  .then((res) => res.json())
  .catch((err) => console.log("Handled error"));
```

---

## Promisifying a Callback-Based Function

Convert callback functions into promises.

Example with setTimeout:

```javascript
function delay(ms) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

delay(1000).then(() => console.log("Done"));
```

Example with fs.readFile:

```javascript
import fs from "fs";

function readFilePromise(path) {
  return new Promise((resolve, reject) => {
    fs.readFile(path, "utf-8", (err, data) => {
      if (err) reject(err);
      else resolve(data);
    });
  });
}
```

---

## Promise.resolve

Creates a resolved promise.

Example:

```javascript
Promise.resolve("Immediate").then(console.log);
```

---

## Promise.reject

Creates a rejected promise.

Example:

```javascript
Promise.reject("Error").catch(console.log);
```

---

## Promise.all

Resolves when all promises succeed, rejects if any fails.

Example:

```javascript
Promise.all([
  Promise.resolve(1),
  Promise.resolve(2)
]).then(console.log);
```

---

## Promise.allSettled

Waits for all promises and returns their status.

Example:

```javascript
Promise.allSettled([
  Promise.resolve("Success"),
  Promise.reject("Fail")
]).then(console.log);
```

---

## Promise.any

Resolves when the first promise succeeds.

Example:

```javascript
Promise.any([
  Promise.reject("Fail"),
  Promise.resolve("Success")
]).then(console.log);
```

---

## Promise.race

Returns the first settled promise (resolve or reject).

Example:

```javascript
Promise.race([
  new Promise((resolve) => setTimeout(() => resolve("Fast"), 100)),
  new Promise((resolve) => setTimeout(() => resolve("Slow"), 1000))
]).then(console.log);
```

---



