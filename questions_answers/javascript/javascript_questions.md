## What is JavaScript? Why is it called a scripting language?
JavaScript is a high-level, interpreted programming language that is primarily used to create interactive and dynamic content on web pages. It allows developers to manipulate the Document Object Model (DOM), handle events, and perform various tasks such as form validation, animations, and asynchronous operations. JavaScript is called a scripting language because it is typically executed in a web browser and is used to "script" the behavior of web pages, enabling developers to add functionality and interactivity without needing to compile code. It is an essential part of modern web development, alongside HTML and CSS.

## What is the difference between var, let and const?
In JavaScript, `var`, `let`, and `const` are used to declare variables, but they have different characteristics:
- `var`: This is the oldest way to declare variables in JavaScript. Variables declared with `var` are function-scoped, meaning they are accessible within the function they are declared in. They can be re-declared and updated, which can lead to unintended consequences if not used carefully.
- `let`: Introduced in ES6, `let` is block-scoped, meaning it is only accessible within the block (e.g., inside a loop or an if statement) it is declared in. Variables declared with `let` can be updated but cannot be re-declared within the same scope, which helps prevent accidental variable overwriting.
- `const`: Also introduced in ES6, `const` is block-scoped like `let`, but it is used to declare variables that cannot be reassigned after their initial assignment. However, if the variable is an object or an array, its properties or elements can still be modified. `const` is useful for declaring constants or values that should not change throughout the program. In summary, `var` is function-scoped and can be re-declared, `let` is block-scoped and can be updated but not re-declared, and `const` is block-scoped and cannot be reassigned after its initial assignment.
`Example:`
```javascript
var x = 10; // function-scoped, can be re-declared and updated
let y = 20; // block-scoped, can be updated but not re-declared
const z = 30; // block-scoped, cannot be reassigned
```

## What is a function? What are arrow functions?
A function in JavaScript is a reusable block of code that performs a specific task or calculates a value. Functions can take parameters, execute code, and return a result. They are fundamental building blocks in JavaScript and are used to organize code, improve readability, and promote code reuse.
Arrow functions, introduced in ES6, are a more concise syntax for writing functions. They are defined using the `=>` syntax and do not have their own `this`, `arguments`, or `super` bindings. Arrow functions are often used for shorter functions or when a function needs to be passed as an argument to another function. They can also help avoid issues with the `this` keyword in certain contexts, such as when working with callbacks or methods in classes.
`Example:`
```javascript
// Regular function
function add(a, b) {
  return a + b;
}
// Arrow function
const add = (a, b) => a + b;
```
In this example, both the regular function and the arrow function perform the same task of adding two numbers, but the arrow function provides a more concise syntax.

## What is the DOM?
The DOM, or Document Object Model, is a programming interface for web documents. It represents the structure of an HTML or XML document as a tree of objects, where each node corresponds to an element, attribute, or piece of text in the document. The DOM allows developers to interact with and manipulate the content, structure, and style of web pages dynamically using JavaScript. Through the DOM, developers can access and modify elements, handle events, and create new elements on the fly, enabling the creation of interactive and dynamic web applications.
For example, using the DOM, you can change the text of a heading element like this:
```javascript
document.getElementById("myHeading").textContent = "New Heading Text";
```
In this example, the `getElementById` method is used to select an element with the ID "myHeading", and the `textContent` property is updated to change the text displayed on the web page.

## What is event bubbling and event capturing?
Event bubbling and event capturing are two phases of event propagation in the DOM. When an event occurs on an element, it can trigger handlers on that element as well as on its ancestors in the DOM tree.
- Event bubbling is the default behavior where the event starts from the target element and propagates upwards through its ancestors until it reaches the root of the DOM tree. In this phase, event handlers on the target element are executed first, followed by handlers on its parent elements.
- Event capturing, on the other hand, is the opposite of bubbling. In this phase, the event starts from the root of the DOM tree and propagates downwards to the target element. Event handlers on ancestor elements are executed before handlers on the target element.
In JavaScript, you can specify whether an event handler should be executed during the capturing phase by passing a third argument to the `addEventListener` method. For example:
```javascript
element.addEventListener("click", handler, true); // Capturing phase
element.addEventListener("click", handler, false); // Bubbling phase (default)
```
In this example, the `true` argument indicates that the event handler should be executed during the capturing phase, while `false` (or omitting the argument) indicates that it should be executed during the bubbling phase. Understanding event propagation is important for managing how events are handled in complex web applications and for preventing unintended side effects when multiple handlers are involved.

## What is the difference between == and ===?
In JavaScript, `==` and `===` are both comparison operators, but they behave differently when comparing values:
- `==` (loose equality) compares two values for equality after performing type coercion. This means that if the values being compared are of different types, JavaScript will attempt to convert them to a common type before making the comparison. For example, `5 == "5"` would return `true` because the string "5" is coerced to the number 5 before the comparison.
- `===` (strict equality) compares two values for equality without performing type coercion. This means that if the values being compared are of different types, the comparison will return `false`. For example, `5 === "5"` would return `false` because the number 5 and the string "5" are of different types.
In general, it is recommended to use `===` for comparisons in JavaScript to avoid unexpected results due to type coercion, and to ensure that both the value and the type are being compared.
`Example:`
```javascript
console.log(5 == "5"); // true (type coercion occurs)
console.log(5 === "5"); // false (no type coercion, different types)
```
In this example, the first comparison using `==` returns `true` because the string "5" is coerced to the number 5, while the second comparison using `===` returns `false` because the types of the values are different (number vs. string).

## What is an array? Name five array methods.
An array in JavaScript is a data structure that can hold a collection of values, which can be of any type (e.g., numbers, strings, objects). Arrays are ordered and indexed, meaning that each element in the array has a specific position (index) starting from 0. Arrays are commonly used to store lists of items and provide various methods for manipulating and accessing the data they contain. Here are five commonly used array methods in JavaScript:
1. `push()`: Adds one or more elements to the end of an array and returns the new length of the array.
2. `pop()`: Removes the last element from an array and returns that element.
3. `shift()`: Removes the first element from an array and returns that element.
4. `unshift()`: Adds one or more elements to the beginning of an array and returns the new length of the array.
5. `map()`: Creates a new array by applying a provided function to each element in the original array.
`Example:`
```javascript
let numbers = [1, 2, 3];
numbers.push(4); // numbers is now [1, 2, 3, 4]
let lastNumber = numbers.pop(); // lastNumber is 4, numbers is now [1, 2, 3]
numbers.unshift(0); // numbers is now [0, 1, 2, 3]
let squaredNumbers = numbers.map(num => num * num); // squaredNumbers is [0, 1, 4, 9]
```
In this example, we demonstrate the use of the `push()`, `pop()`, `unshift()`, and `map()` methods to manipulate the `numbers` array and create a new array of squared values.

## What is a callback function?
A callback function in JavaScript is a function that is passed as an argument to another function and is executed after some operation has been completed. Callback functions are commonly used for handling asynchronous operations, such as making API calls, reading files, or responding to user events. They allow developers to specify what should happen once a certain task is finished, without blocking the execution of the rest of the code.
For example, when making an API call, you can pass a callback function that will be executed once the response is received:
```javascript
function fetchData(url, callback) {
  // Simulate an API call
  setTimeout(() => {
    const data = { name: "John", age: 30 }; // Simulated response data
    callback(data); // Call the callback function with the data
  }, 1000);
}
fetchData("https://api.example.com/user", function(response) {
  console.log("User data:", response);
});
```
In this example, the `fetchData` function simulates an API call using `setTimeout`. The callback function is passed as an argument and is executed once the simulated response data is ready, allowing us to log the user data to the console. Callback functions are essential for managing asynchronous code and ensuring that certain actions are performed after specific tasks are completed.

## What is asynchronous JavaScript?
Asynchronous JavaScript refers to the ability of JavaScript to perform tasks without blocking the main thread of execution. This means that while JavaScript is waiting for a long-running operation (such as an API call, file reading, or a timer) to complete, it can still respond to user interactions and execute other code. Asynchronous programming in JavaScript is typically achieved using callbacks, promises, or async/await syntax.
For example, using promises, you can handle asynchronous operations like this:
```javascriptfunction fetchData(url) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const data = { name: "John", age: 30 }; // Simulated response data
      resolve(data); // Resolve the promise with the data
    }, 1000);
  });
}
fetchData("https://api.example.com/user")
  .then(response => {
    console.log("User data:", response);
  })
  .catch(error => {
    console.error("Error fetching data:", error);
  });
```
In this example, the `fetchData` function returns a promise that simulates an API call. The `then` method is used to handle the resolved value (the user data), while the `catch` method is used to handle any potential errors. Asynchronous JavaScript allows for more efficient and responsive applications by enabling non-blocking operations, which is crucial for tasks that may take time to complete.

## What is the difference between localStorage, sessionStorage, and cookies?
`localStorage`, `sessionStorage`, and cookies are all mechanisms for storing data on the client side in web browsers, but they have different characteristics and use cases:
- `localStorage`: This is a web storage API that allows you to store key-value pairs in the browser with no expiration time. Data stored in `localStorage` persists even after the browser is closed and reopened. It is typically used for storing data that needs to be retained across sessions, such as user preferences or application state.
- `sessionStorage`: This is another web storage API that also allows you to store key-value pairs, but the data is only available for the duration of the page session. Once the browser tab is closed, the data stored in `sessionStorage` is cleared. It is useful for storing temporary data that should not persist beyond the current session, such as form inputs or temporary state.
- Cookies: Cookies are small pieces of data that are stored in the browser and sent to the server with every HTTP request. They have an expiration date and can be set to persist across sessions or be deleted when the browser is closed. Cookies are commonly used for authentication, tracking user behavior, and storing small amounts of data that need to be sent to the server. However, they have size limitations (typically around 4KB) and can be less secure than `localStorage` or `sessionStorage` if not handled properly.
In summary, `localStorage` is for persistent data that should remain across sessions, `sessionStorage` is for temporary data that should only last for the current session, and cookies are for small pieces of data that need to be sent to the server with each request.

## What is hoisting?
Hoisting is a JavaScript mechanism where variable and function declarations are moved to the top of their containing scope during the compilation phase. This means that you can use variables and functions before they are declared in the code. However, only the declarations are hoisted, not the initializations. For example:
```javascript
console.log(x); // undefined (due to hoisting)
var x = 5;
```
In this example, the variable `x` is hoisted to the top of its scope, but its initialization with the value `5` is not. Therefore, when we try to log `x` before it is initialized, it returns `undefined`. Hoisting can lead to unexpected behavior if not understood properly, so it's important to be aware of how it works when writing JavaScript code.

## What is scope? Explain global, local, and block scope.
Scope in JavaScript refers to the accessibility of variables and functions in different parts of the code. There are three main types of scope: global scope, local scope, and block scope.
- Global Scope: Variables and functions declared in the global scope are accessible from anywhere in the code. They are typically declared outside of any function or block. For example:
```javascript
var globalVar = "I am a global variable";
function example() {
  console.log(globalVar); // Accessible here
}
example(); // Logs: I am a global variable
```
- Local Scope: Variables and functions declared within a function are in local scope. They are only accessible within that function and cannot be accessed from outside. For example:
```javascript
function example() {
  var localVar = "I am a local variable";
  console.log(localVar); // Accessible here
}
example(); // Logs: I am a local variable
console.log(localVar); // Uncaught ReferenceError: localVar is not defined
```
- Block Scope: Variables declared with `let` or `const` within a block (e.g., inside an if statement or a loop) are in block scope. They are only accessible within that block and cannot be accessed from outside. For example:
```javascript
if (true) {
  let blockVar = "I am a block-scoped variable";
  console.log(blockVar); // Accessible here
}
console.log(blockVar); // Uncaught ReferenceError: blockVar is not defined
```
In this example, `blockVar` is only accessible within the if block where it is declared, and trying to access it outside of that block results in a ReferenceError. Understanding scope is crucial for managing variable accessibility and avoiding unintended side effects in JavaScript code.

## What is closure?
A closure in JavaScript is a function that has access to its own scope, the scope of the outer function, and the global scope. Closures are created when a function is defined inside another function and allows the inner function to access variables and parameters of the outer function even after the outer function has finished executing. This is because the inner function retains a reference to the outer function's scope, allowing it to access and manipulate those variables.
For example:
```javascript
function outerFunction() {
  let outerVariable = "I am from the outer function";
  
  function innerFunction() {
    console.log(outerVariable); // Accessing the outer variable
  }
  
  return innerFunction; // Returning the inner function
}
const closureExample = outerFunction(); // outerFunction is executed, and innerFunction is returned
closureExample(); // Logs: I am from the outer function
```
In this example, `innerFunction` is a closure that has access to the `outerVariable` defined in `outerFunction`. Even after `outerFunction` has finished executing, `innerFunction` can still access and log the value of `outerVariable`, demonstrating how closures allow functions to retain access to their lexical scope. Closures are commonly used for data privacy, creating function factories, and implementing callbacks in JavaScript.

## What is the difference between synchronous and asynchronous code?
Synchronous code is executed sequentially, meaning that each operation must complete before the next one begins. In synchronous programming, if a task takes a long time to complete (such as a network request or a heavy computation), it will block the execution of the entire program until it finishes. This can lead to unresponsive applications, especially in web development where user interactions are expected to be smooth and responsive.
Asynchronous code, on the other hand, allows multiple operations to be executed concurrently without blocking the main thread. In asynchronous programming, tasks that take time to complete can be initiated and then the program can continue executing other code while waiting for those tasks to finish. This is typically achieved using callbacks, promises, or async/await syntax in JavaScript. Asynchronous code is essential for handling operations like API calls, file reading, and timers without freezing the user interface.
For example, using asynchronous code with promises:
```javascript
function fetchData(url) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const data = { name: "John", age: 30 }; // Simulated response data
      resolve(data); // Resolve the promise with the data
    }, 1000);
  });
}
fetchData("https://api.example.com/user")
  .then(response => {
    console.log("User data:", response);
  })
  .catch(error => {
    console.error("Error fetching data:", error);
  });
```
In this example, the `fetchData` function simulates an asynchronous operation using a promise. The program can continue executing other code while waiting for the simulated API call to complete, allowing for a more responsive user experience. In contrast, if this were done synchronously, the program would be blocked until the data is fetched, which could lead to a poor user experience.

## What are promises?
Promises in JavaScript are objects that represent the eventual completion (or failure) of an asynchronous operation and its resulting value. A promise can be in one of three states: pending, fulfilled, or rejected. When a promise is created, it starts in the pending state. If the asynchronous operation completes successfully, the promise is fulfilled with a value. If it fails, the promise is rejected with a reason (error). Promises provide a cleaner and more manageable way to handle asynchronous operations compared to traditional callbacks, especially when dealing with multiple asynchronous tasks or when chaining operations together.
Promises can be created using the `Promise` constructor, and they can be consumed using the `then` and `catch` methods. For example:
```javascript
function fetchData(url) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const data = { name: "John", age: 30 }; // Simulated response data
      resolve(data); // Resolve the promise with the data
    }, 1000);
  });
}
fetchData("https://api.example.com/user")
  .then(response => {
    console.log("User data:", response);
  })
  .catch(error => {
    console.error("Error fetching data:", error);
  });
```
In this example, the `fetchData` function returns a promise that simulates an asynchronous operation. The `then` method is used to handle the resolved value (the user data), while the `catch` method is used to handle any potential errors. Promises allow for better error handling and more readable code when working with asynchronous operations in JavaScript.

## What is async/await?
Async/await is a syntactic sugar in JavaScript that provides a more readable and straightforward way to work with promises and asynchronous code. It allows developers to write asynchronous code that looks and behaves like synchronous code, making it easier to understand and maintain. The `async` keyword is used to declare an asynchronous function, while the `await` keyword is used to pause the execution of the function until a promise is resolved or rejected.
When an `async` function is called, it returns a promise. Inside the function, you can use `await` to wait for a promise to resolve before proceeding with the next line of code. This helps avoid callback hell and makes it easier to handle asynchronous operations in a more linear and intuitive manner.
For example:
```javascript
async function fetchData(url) {
  try {
    const response = await fetch(url); // Wait for the fetch promise to resolve
    const data = await response.json(); // Wait for the response to be parsed as JSON
    console.log("User data:", data);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}
fetchData("https://api.example.com/user");
```
In this example, the `fetchData` function is declared as an async function. Inside the function, we use `await` to wait for the `fetch` promise to resolve and then wait for the response to be parsed as JSON. The try/catch block is used to handle any potential errors that may occur during the asynchronous operations. Async/await provides a cleaner and more readable way to work with asynchronous code compared to traditional promise chaining or callbacks.

## What is the event loop?
The event loop is a fundamental concept in JavaScript that allows for non-blocking, asynchronous programming. It is responsible for managing the execution of code, handling events, and processing asynchronous tasks. The event loop continuously checks the call stack and the task queue to determine what code to execute next. When a function is called, it is added to the call stack. If the function contains asynchronous operations (like setTimeout, fetch, or promises), those operations are offloaded to the browser's APIs, and the function is removed from the call stack. Once the asynchronous operation is completed, its callback or promise resolution is added to the task queue. The event loop then checks if the call stack is empty and, if so, it takes the next task from the task queue and pushes it onto the call stack for execution. This mechanism allows JavaScript to handle multiple tasks concurrently without blocking the main thread, enabling responsive user interfaces and efficient handling of I/O operations.
For example:
```javascript
console.log("Start");
setTimeout(() => {
  console.log("This is an asynchronous task");
}, 1000);
console.log("End");
```
In this example, the output will be:
```
Start
End
This is an asynchronous task
```
This demonstrates how the event loop allows the synchronous code ("Start" and "End") to execute immediately, while the asynchronous task (the setTimeout callback) is executed after a delay, without blocking the main thread.

## What is debouncing and throttling?
Debouncing and throttling are techniques used to control the rate at which a function is executed in response to events, such as user input or window resizing, to improve performance and prevent excessive function calls.
- Debouncing is a technique that ensures a function is only executed after a certain amount of time has passed since the last time it was invoked. This is useful for scenarios like search input, where you want to wait until the user has stopped typing before making an API call. For example:
```javascript
function debounce(func, delay) {
    let timeoutId;
    return function(...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => {
            func.apply(this, args);
        }, delay);
    };
}
```
- Throttling, on the other hand, ensures that a function is only executed once in a specified time interval, regardless of how many times it is triggered. This is useful for scenarios like window resizing or scrolling, where you want to limit the number of times a function is called to improve performance. For example:
```javascript
function throttle(func, limit) {
    let lastFunc;
    let lastRan;
    return function(...args) {
        if (!lastRan) {
            func.apply(this, args);
            lastRan = Date.now();
        } else {
            clearTimeout(lastFunc);
            lastFunc = setTimeout(() => {
                if ((Date.now() - lastRan) >= limit) {
                    func.apply(this, args);
                    lastRan = Date.now();
                }
            }, limit - (Date.now() - lastRan));
        }
    };
}
```
In summary, debouncing delays the execution of a function until a certain amount of time has passed since the last invocation, while throttling limits the execution of a function to once in a specified time interval. Both techniques are essential for optimizing performance and improving user experience in web applications.

## What is destructuring?
Destructuring is a convenient way to extract values from arrays or properties from objects and assign them to variables in a more concise and readable manner. It allows you to unpack values from arrays or objects into distinct variables, making it easier to work with complex data structures.
For example, with arrays:
```javascript
const numbers = [1, 2, 3];
const [a, b, c] = numbers;
console.log(a); // 1
console.log(b); // 2
console.log(c); // 3
```
With objects:
```javascript
const person = { name: "John", age: 30 };
const { name, age } = person;
console.log(name); // John
console.log(age); // 30
```
In this example, we use destructuring to extract values from an array and an object. The variables `a`, `b`, and `c` are assigned the values from the `numbers` array, while the variables `name` and `age` are assigned the corresponding properties from the `person` object. Destructuring can also be used with nested objects and arrays, making it a powerful tool for working with complex data structures in JavaScript.

## What is spread and rest operator?
The spread operator (`...`) and rest operator (`...`) are both represented by three dots, but they serve different purposes in JavaScript.
- The spread operator is used to expand an iterable (like an array or an object) into individual elements. It is commonly used for copying arrays or objects, merging arrays, or passing elements as arguments to a function. For example:
```javascript
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5]; // Merging arr1 with additional elements
console.log(arr2); // [1, 2, 3, 4, 5]
const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3 }; // Copying obj1 and adding a new property
console.log(obj2); // { a: 1, b: 2, c: 3 }
```
- The rest operator is used to collect multiple elements into a single variable. It is often used in function parameters to gather remaining arguments into an array or to collect remaining properties of an object. For example:
```javascript
function sum(...numbers) {
    return numbers.reduce((acc, curr) => acc + curr, 0);
}
console.log(sum(1, 2, 3)); // 6
const { a, ...rest } = { a: 1, b: 2, c: 3 };
console.log(a); // 1
console.log(rest); // { b: 2, c: 3 }
```
In this example, the spread operator is used to merge arrays and copy objects, while the rest operator is used to gather function arguments into an array and to collect remaining properties of an object. Both operators provide a more concise and flexible way to work with arrays and objects in JavaScript.

## What is the JavaScript execution context?
The JavaScript execution context is an abstract concept that represents the environment in which JavaScript code is executed. It consists of three main components: the variable environment, the scope chain, and the `this` keyword. The execution context is created whenever a function is invoked or when the global code is executed. It determines how variables and functions are accessed and how the `this` keyword behaves within that context. There are two types of execution contexts: global execution context (created when the script starts) and function execution context (created when a function is called). Each execution context has its own variable environment, which holds variables, function declarations, and parameters, as well as a reference to its outer environment through the scope chain. Understanding execution contexts is crucial for grasping how JavaScript handles variable scope, function calls, and the behavior of `this`.
For example:
```javascript
function outerFunction() {
    var outerVariable = "I am from the outer function";
    
    function innerFunction() {
        console.log(outerVariable); // Accessing the outer variable
    }
    
    innerFunction(); // Logs: I am from the outer function
}
outerFunction();
```
In this example, when `outerFunction` is called, a new execution context is created for it. Inside `outerFunction`, another execution context is created for `innerFunction` when it is invoked. The `innerFunction` has access to the variable `outerVariable` through the scope chain, demonstrating how execution contexts manage variable access and function calls in JavaScript.

## Explain call stack and memory heap.
The call stack and memory heap are two important components of the JavaScript runtime environment that manage the execution of code and memory allocation.
- The call stack is a data structure that keeps track of the function calls in a program. When a function is called, it is added to the top of the call stack. The JavaScript engine executes the function at the top of the stack, and when that function finishes executing, it is removed from the stack. If a function calls another function, the new function is added to the top of the stack, and this process continues until all functions have been executed. If the call stack exceeds its limit (e.g., due to infinite recursion), it results in a "stack overflow" error.
- The memory heap is a region of memory used for dynamic memory allocation. It is where objects, arrays, and functions are stored in JavaScript. When a new object or function is created, it is allocated memory in the heap. The JavaScript engine manages this memory and performs garbage collection to free up memory that is no longer in use. The memory heap allows for flexible memory management, as it can grow and shrink as needed during the execution of a program.
In summary, the call stack manages the execution of function calls in a last-in-first-out (LIFO) manner, while the memory heap is responsible for storing objects and functions in memory. Both components are essential for the proper functioning of JavaScript programs, as they handle the execution flow and memory management respectively.

## What is garbage collection?
Garbage collection in JavaScript is the process of automatically freeing up memory that is no longer being used by the program. Since JavaScript is a high-level language, it abstracts away memory management from the developer, allowing the JavaScript engine to handle it automatically. The garbage collector identifies and removes objects that are no longer reachable or referenced in the code, meaning that there are no active references to those objects. This helps prevent memory leaks and ensures that the application does not consume more memory than necessary. The most common algorithm used for garbage collection in JavaScript is mark-and-sweep, which marks all reachable objects and then sweeps through the memory to collect unmarked (unreachable) objects. Understanding garbage collection is important for optimizing performance and managing memory effectively in JavaScript applications.
For example, if you create an object and then set it to null, the garbage collector will eventually free up the memory used by that object:
```javascript
let myObject = { name: "John", age: 30 };
myObject = null; // The object is now unreachable and can be garbage collected
```
In this example, the `myObject` variable initially holds a reference to an object. When we set `myObject` to null, the reference to the object is removed, making it unreachable. The garbage collector will eventually identify that the object is no longer in use and will free up the memory allocated for it. This process helps ensure that memory is efficiently managed in JavaScript applications.

## What is currying?
Currying is a functional programming technique in JavaScript where a function with multiple arguments is transformed into a sequence of functions that each take a single argument. This allows for partial application of functions, meaning that you can create new functions by fixing some of the arguments of the original function. Currying can help improve code readability and reusability by allowing you to create more specific functions from general ones.
For example, consider a simple function that adds two numbers:
```javascript
function add(a, b) {
    return a + b;
}
```
Using currying, we can transform this function into a curried version:
```javascript
function curriedAdd(a) {
    return function(b) {
        return a + b;
    };
}
```
Now, we can create new functions by partially applying the curried function:
```javascript
const add5 = curriedAdd(5); // This creates a new function that adds 5 to its argument
console.log(add5(10)); // Logs: 15
```
In this example, `curriedAdd` is a curried version of the `add` function. By calling `curriedAdd(5)`, we create a new function `add5` that takes a single argument and adds 5 to it. Currying allows for more flexible and reusable code, as you can easily create new functions by partially applying existing ones.

## What is memoization?
Memoization is an optimization technique in JavaScript that involves caching the results of expensive function calls and returning the cached result when the same inputs occur again. This can significantly improve the performance of functions that are called multiple times with the same arguments, as it avoids redundant calculations. Memoization is often used in recursive functions, such as those that calculate Fibonacci numbers, where the same inputs can lead to repeated calculations.
For example, consider a recursive function to calculate the Fibonacci sequence:
```javascript
function fibonacci(n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}
```
This function can be inefficient for large values of `n` due to repeated calculations. By using memoization, we can optimize it:
```javascript
function memoizedFibonacci() {
    const cache = {};
    return function fib(n) {
        if (n in cache) {
            return cache[n]; // Return cached result if available
        }
        if (n <= 1) return n;
        cache[n] = fib(n - 1) + fib(n - 2); // Cache the result before returning
        return cache[n];
    };
}
const fibonacci = memoizedFibonacci();
console.log(fibonacci(50)); // This will be much faster than the non-memoized version
```
In this example, the `memoizedFibonacci` function creates a cache object to store previously calculated results. The inner `fib` function checks if the result for a given `n` is already in the cache before performing the recursive calculations. If it is, it returns the cached result, otherwise, it calculates it, stores it in the cache, and then returns it. This approach significantly reduces the time complexity of the Fibonacci function from exponential to linear.

## What is deep copy vs shallow copy?
A deep copy and a shallow copy are two different ways of copying objects in JavaScript, and they differ in how they handle nested objects and references.
- A shallow copy creates a new object that is a copy of the original object, but it only copies the top-level properties. If the original object contains nested objects, the shallow copy will still reference those nested objects rather than creating new ones. This means that changes to the nested objects in the shallow copy will affect the original object and vice versa. For example:
```javascript
const original = { name: "John", address: { city: "New York" } };
const shallowCopy = { ...original };
shallowCopy.address.city = "Los Angeles";
console.log(original.address.city); // Logs: Los Angeles (because it's a shallow copy)
```
- A deep copy, on the other hand, creates a new object that is a complete copy of the original object, including all nested objects. This means that changes to the nested objects in the deep copy will not affect the original object. Deep copying can be achieved using various methods, such as JSON serialization or recursive copying. For example:
```javascript
const original = { name: "John", address: { city: "New York" } };
const deepCopy = JSON.parse(JSON.stringify(original));
deepCopy.address.city = "Los Angeles";
console.log(original.address.city); // Logs: New York (because it's a deep copy)
```
In this example, the `deepCopy` is created using JSON serialization, which creates a new object with all nested objects copied. As a result, changing the `city` property in `deepCopy` does not affect the `original` object. In summary, a shallow copy only copies the top-level properties and references nested objects, while a deep copy creates a completely independent copy of the original object, including all nested objects.

## What is the difference between Object.freeze() and Object.seal()?
`Object.freeze()` and `Object.seal()` are both methods in JavaScript that are used to control the mutability of objects, but they have different effects on the object properties.
- `Object.freeze()`: This method makes an object immutable. It prevents any changes to the object, including adding new properties, deleting existing properties, or modifying the values of existing properties. Once an object is frozen, it cannot be unfrozen. For example:
```javascript
const obj = { name: "John", age: 30 };
Object.freeze(obj);
obj.name = "Jane"; // This will not change the name property
console.log(obj.name); // Logs: John
```
- `Object.seal()`: This method prevents new properties from being added to an object and marks all existing properties as non-configurable. However, it still allows the values of existing properties to be modified. For example:
```javascript
const obj = { name: "John", age: 30 };
Object.seal(obj);
obj.name = "Jane"; // This will change the name property
console.log(obj.name); // Logs: Jane
obj.address = "123 Main St"; // This will not add a new property
console.log(obj.address); // Logs: undefined
```
In summary, `Object.freeze()` makes an object completely immutable, while `Object.seal()` allows for modification of existing properties but prevents the addition of new properties. Both methods are useful for controlling the mutability of objects in JavaScript, depending on the level of immutability required.

## What are Web Workers?
Web Workers are a feature in JavaScript that allows for running scripts in the background, separate from the main execution thread of a web application. This is particularly useful for performing computationally intensive tasks without blocking the user interface, ensuring that the application remains responsive. Web Workers operate in a different context than the main thread, meaning they do not have access to the DOM or certain JavaScript APIs, but they can communicate with the main thread using a messaging system. This allows developers to offload heavy processing tasks to Web Workers while still being able to update the UI or handle user interactions in the main thread.
For example, you can create a Web Worker to perform a long-running calculation:
```javascript
// main.js
const worker = new Worker('worker.js');
worker.postMessage('start'); // Send a message to the worker to start processing
worker.onmessage = function(event) {
    console.log('Result from worker:', event.data); // Handle the result from the worker
};
// worker.js
self.onmessage = function(event) {
    if (event.data === 'start') {
        // Perform a long-running calculation
        let result = 0;
        for (let i = 0; i < 1e9; i++) {
            result += i;
        }
        self.postMessage(result); // Send the result back to the main thread
    }
};
```
In this example, the main thread creates a Web Worker and sends a message to start a long-running calculation. The worker performs the calculation in the background and sends the result back to the main thread once it is complete. This allows the main thread to remain responsive while the worker is processing the task. Web Workers are an essential tool for improving performance and user experience in web applications that require heavy computations or background processing.

## What is the difference between map(), filter(), and reduce()?
`map()`, `filter()`, and `reduce()` are all array methods in JavaScript that are used to manipulate and transform arrays, but they serve different purposes:
- `map()`: This method creates a new array by applying a provided function to each element in the original array. It returns a new array of the same length as the original, where each element is the result of the function applied to the corresponding element in the original array. For example:
```javascript
const numbers = [1, 2, 3];
const squared = numbers.map(num => num * num);
console.log(squared); // Logs: [1, 4, 9]
```
- `filter()`: This method creates a new array with all elements that pass a test implemented by the provided function. It returns a new array containing only the elements that satisfy the condition specified in the function. For example:
```javascript
const numbers = [1, 2, 3, 4, 5];
const evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // Logs: [2, 4]
```
- `reduce()`: This method executes a reducer function on each element of the array, resulting in a single output value. It takes an accumulator and the current value as arguments and returns the accumulated result after processing all elements in the array. For example:
```javascript
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((accumulator, currentValue) => accumulator + currentValue, 0);
console.log(sum); // Logs: 10
```
In summary, `map()` is used for transforming each element of an array, `filter()` is used for selecting elements based on a condition, and `reduce()` is used for reducing an array to a single value by applying a function cumulatively to its elements. Each of these methods provides a powerful way to manipulate arrays in JavaScript, allowing for more concise and readable code.

## What is module bundling?
Module bundling is the process of taking multiple JavaScript files (modules) and combining them into a single file (or a few files) that can be included in a web application. This is typically done to improve performance by reducing the number of HTTP requests needed to load the application, as well as to manage dependencies between modules. Module bundlers, such as Webpack, Rollup, and Parcel, analyze the dependency graph of the modules and create optimized bundles that can be efficiently loaded by the browser. They also often include features like code splitting, tree shaking, and hot module replacement to further enhance performance and development experience. Module bundling is an essential part of modern JavaScript development, especially for large applications with many dependencies.
For example, if you have multiple JavaScript files that import each other, a module bundler can analyze these imports and create a single bundle that includes all the necessary code. This allows you to write modular code while still delivering an optimized bundle to the client. Additionally, module bundlers can handle various types of assets (like CSS, images, etc.) and can be configured to perform tasks like minification and transpilation, making them a crucial tool in the modern JavaScript development workflow.

## What is execution order between `setTimeout`, `Promise`, and `async/await`?
The execution order between `setTimeout`, `Promise`, and `async/await` in JavaScript is determined by the event loop and the microtask queue. When a `setTimeout` is called, it schedules a callback to be executed after a specified delay, and this callback is placed in the task queue. Promises, on the other hand, are part of the microtask queue, which has a higher priority than the task queue. When a Promise is resolved or rejected, its associated callbacks are placed in the microtask queue and will be executed before any tasks in the task queue. The `async/await` syntax is built on top of Promises, so when an `async` function is called, it returns a Promise. When an `await` expression is encountered, it pauses the execution of the async function until the Promise is resolved or rejected, at which point the rest of the function continues executing as a microtask. In summary, the execution order is as follows: first, all microtasks (including Promise callbacks and async function continuations) are executed before any tasks from the task queue (such as `setTimeout` callbacks) are processed.
`Example of execution order between setTimeout, Promise, and async/await:`
```javascript
console.log('Start');
setTimeout(() => {
  console.log('setTimeout callback'); // This will be executed after the current call stack is empty and all microtasks are processed
}, 0);
Promise.resolve().then(() => {
  console.log('Promise callback'); // This will be executed before the setTimeout callback because it is a microtask
});
async function asyncFunction() {
  console.log('Async function start');
  await Promise.resolve();
  console.log('Async function end'); // This will be executed after the Promise callback because it is a continuation of the async function
}
asyncFunction();
```
In this example, the output will be:
```
Start
Async function start
Promise callback
Async function end
setTimeout callback
```
This demonstrates the execution order where the `Promise` callback is executed before the `setTimeout` callback, and the continuation of the `async` function is executed after the `Promise` callback but before the `setTimeout` callback.

## What is idempotency in APIs (JS perspective)?
Idempotency in APIs refers to the property of an operation where performing the same operation multiple times has the same effect as performing it once. In the context of JavaScript and APIs, an idempotent API endpoint is one that can be called multiple times with the same parameters without causing unintended side effects or changes in state. This is particularly important for operations that modify data, such as creating, updating, or deleting resources. Idempotent APIs help ensure that clients can safely retry requests in case of network failures or other issues without worrying about duplicate actions being performed.
`Example of idempotency in APIs:`
```javascript
// Example of an idempotent API endpoint for updating a resource
app.put('/api/resource/:id', (req, res) => {
  const resourceId = req.params.id;
  const newData = req.body;
  
  // Update the resource with the new data
  updateResource(resourceId, newData)
    .then(() => {
      res.status(200).send('Resource updated successfully');
    })
    .catch((error) => {
      res.status(500).send('Error updating resource');
    });
});
```
In this example, the `PUT` endpoint for updating a resource is designed to be idempotent. If a client sends the same update request multiple times with the same `resourceId` and `newData`, the outcome will be the same: the resource will be updated to the new data, and the response will indicate success. This allows clients to safely retry the request if needed without worrying about unintended consequences or duplicate updates.

## What is structuredClone()?
`structuredClone()` is a built-in JavaScript function that creates a deep copy of a given value, including complex data structures like objects, arrays, and even certain types of functions. It is designed to handle circular references and can clone a wide variety of data types, including primitives, objects, arrays, Maps, Sets, and more. The `structuredClone()` function is particularly useful for creating deep copies of data without the need for external libraries or custom cloning functions. It is part of the HTML Living Standard and is supported in modern browsers.
`Example of using structuredClone():`
```javascript
const original = {
  name: "John",
  age: 30,
  address: {
    city: "New York",
    zip: "10001"
  }
};
const cloned = structuredClone(original);
cloned.name = "Jane";
cloned.address.city = "Los Angeles";
console.log(original.name); // Logs: John (original object remains unchanged)
console.log(original.address.city); // Logs: New York (original object remains unchanged)
console.log(cloned.name); // Logs: Jane (cloned object has the new name)
console.log(cloned.address.city); // Logs: Los Angeles (cloned object has the new city)
```
In this example, we use `structuredClone()` to create a deep copy of the `original` object. Modifying the properties of the `cloned` object does not affect the `original` object, demonstrating that a true deep copy has been made. This function is particularly useful for scenarios where you need to duplicate complex data structures without worrying about shared references or unintended side effects.

## What is dynamic import?
Dynamic import is a feature in JavaScript that allows you to load modules asynchronously at runtime, rather than at the initial load time of the application. This is achieved using the `import()` function, which returns a promise that resolves to the module being imported. Dynamic imports are useful for code-splitting and lazy-loading modules, which can improve the performance of web applications by reducing the initial load time and only loading code when it is needed.
`Example of using dynamic import:`
```javascript
function loadModule(moduleName) {
  import(`./modules/${moduleName}.js`)
    .then(module => {
      // Use the imported module
      module.someFunction();
    })
    .catch(error => {
      console.error('Error loading module:', error);
    });
}
loadModule('myModule'); // This will dynamically import the myModule.js file
```
In this example, the `loadModule` function takes a `moduleName` as an argument and uses the `import()` function to dynamically load the corresponding module from the `./modules/` directory. The imported module can then be used within the `.then()` block, and any errors that occur during the import process are handled in the `.catch()` block. Dynamic imports allow for more efficient loading of code and can help improve the performance of web applications by only loading what is necessary when it is needed.

## What is tail call optimization?
Tail call optimization is a technique used by JavaScript engines to optimize recursive function calls that are in tail position. A tail call is a function call that is the last operation performed in a function before it returns. When a function makes a tail call, the JavaScript engine can optimize the call by reusing the current function's stack frame instead of creating a new one for the called function. This allows for more efficient memory usage and can prevent stack overflow errors in cases of deep recursion. Tail call optimization is particularly beneficial for functions that involve recursive calls, such as those that process linked lists or perform mathematical calculations.
`Example of tail call optimization:`
```javascript
function factorial(n, acc = 1) {
  if (n <= 1) return acc;
  return factorial(n - 1, n * acc); // Tail call
}
console.log(factorial(5)); // Logs: 120
```
In this example, the `factorial` function is defined in a way that the recursive call to `factorial` is the last operation performed in the function (tail call). The JavaScript engine can optimize this tail call by reusing the same stack frame for each recursive call, allowing it to compute the factorial of large numbers without running into a stack overflow error. Tail call optimization is an important feature for improving the performance and reliability of recursive functions in JavaScript.

## What is optional chaining?
Optional chaining is a feature in JavaScript that allows you to safely access nested properties of an object without having to check for the existence of each level of the object hierarchy. It is denoted by the `?.` operator and provides a way to handle cases where a property may be `null` or `undefined`. When you use optional chaining, if any part of the chain is `null` or `undefined`, the entire expression will short-circuit and return `undefined` instead of throwing an error. This can help prevent runtime errors and make your code more concise and easier to read.
`Example of using optional chaining:`
```javascript
const user = {
  name: "John",
  address: {
    city: "New York"
  }
};
console.log(user?.address?.city); // Logs: New York (accessing nested property safely)
console.log(user?.contact?.email); // Logs: undefined (contact is undefined, but no error is thrown)
```
In this example, we use optional chaining to access the `city` property of the `address` object safely. If the `address` property were `null` or `undefined`, the expression would return `undefined` instead of throwing an error. Similarly, when trying to access the `email` property of the `contact` object, which does not exist, it returns `undefined` without causing a runtime error. Optional chaining is a powerful feature that helps improve the robustness and readability of your code when dealing with complex objects.

## What is nullish coalescing?
Nullish coalescing is a feature in JavaScript that provides a way to handle `null` or `undefined` values in expressions. It is denoted by the `??` operator and allows you to specify a default value that will be used if the left-hand side of the operator is `null` or `undefined`. This is particularly useful for providing fallback values without having to check for falsy values like `0`, `''`, or `false`, which are not considered nullish. The nullish coalescing operator only considers `null` and `undefined` as nullish, making it a more precise way to handle default values in certain situations.
`Example of using nullish coalescing:`
```javascript
const userInput = null;
const defaultValue = "Default Value";
const result = userInput ?? defaultValue; // result will be "Default Value" because userInput is null
console.log(result); // Logs: Default Value
const anotherInput = 0;
const anotherResult = anotherInput ?? defaultValue; // anotherResult will be 0 because 0 is not nullish
console.log(anotherResult); // Logs: 0
```
In this example, we use the nullish coalescing operator to provide a default value for `userInput` when it is `null`. The `result` variable will be assigned the value of `defaultValue` because `userInput` is `null`. However, when we use the operator with `anotherInput`, which is `0`, it does not consider `0` as nullish, so `anotherResult` will be assigned the value of `0`. This demonstrates how nullish coalescing allows for more precise handling of default values based on whether a value is truly nullish or just falsy.

## What is `runtime` vs `compile` time in JS?
Runtime and compile time are two different phases in the lifecycle of a JavaScript program. Compile time refers to the phase when the JavaScript code is being parsed and compiled by the JavaScript engine. During this phase, the engine checks for syntax errors, creates an abstract syntax tree (AST), and prepares the code for execution. Compile time is when variable declarations are hoisted, and function declarations are processed. On the other hand, runtime refers to the phase when the compiled code is actually executed. During runtime, the JavaScript engine executes the code line by line, manages memory, handles events, and performs operations based on the logic defined in the code. Runtime is when variables are assigned values, functions are called, and any dynamic behavior of the program occurs. Understanding the distinction between compile time and runtime is important for debugging and optimizing JavaScript code effectively.
For example, consider the following code:
```javascript
console.log(x); // This will log 'undefined' due to hoisting (compile time)
var x = 10; // Variable declaration is hoisted, but assignment happens at runtime
function foo() {
    console.log("Hello, World!"); // This function is processed at compile time
}
foo(); // This will log "Hello, World!" at runtime
```
In this example, the variable `x` is declared using `var`, which means it is hoisted to the top of its scope during compile time. However, the assignment of `10` to `x` happens at runtime. As a result, when we log `x` before the assignment, it outputs `undefined`. The function `foo` is also processed at compile time, but it is executed at runtime when we call it, resulting in the output "Hello, World!". This illustrates the difference between compile time and runtime in JavaScript.

## What is memory profiling in JS?
Memory profiling in JavaScript is the process of analyzing and optimizing the memory usage of a JavaScript application. It involves identifying memory leaks, understanding how memory is allocated and deallocated, and optimizing the performance of the application by managing memory more efficiently. Memory profiling can be done using various tools and techniques, such as browser developer tools (like Chrome DevTools), which provide features for tracking memory usage, taking heap snapshots, and analyzing memory allocation over time. By using memory profiling, developers can identify areas of their code that may be consuming excessive memory or causing memory leaks, and make necessary adjustments to improve the overall performance and stability of their applications.
For example, in Chrome DevTools, you can use the Memory panel to take heap snapshots and analyze memory usage. This allows you to see how much memory is being used by different objects and identify any potential memory leaks. You can also use the Timeline panel to track memory allocation over time and see how it changes as you interact with your application. By regularly profiling your application's memory usage, you can ensure that it remains efficient and responsive, especially as it grows in complexity.

## What is event delegation?
Event delegation is a technique in JavaScript that allows you to handle events on a parent element instead of attaching event listeners to individual child elements. This is achieved by taking advantage of event bubbling, where an event propagates up the DOM tree from the target element to its ancestors. By attaching a single event listener to a common ancestor, you can manage events for multiple child elements efficiently, especially when dealing with dynamic content that may be added or removed from the DOM. Event delegation can improve performance and reduce memory usage by minimizing the number of event listeners needed in your application.
`Example of event delegation:`
```javascript
// Instead of attaching event listeners to each button, we attach one listener to the parent element
const parentElement = document.getElementById('buttonContainer');
parentElement.addEventListener('click', function(event) {
  if (event.target && event.target.matches('button')) {
    console.log('Button clicked:', event.target.textContent);
  }
});
```
In this example, we attach a single click event listener to the `parentElement` that contains multiple buttons. When any button is clicked, the event listener checks if the event target matches the selector for a button and then logs the text content of the clicked button. This approach allows us to manage events for all buttons within the container without needing to attach individual listeners to each button, making it more efficient and easier to maintain, especially when buttons are dynamically added or removed from the DOM.

