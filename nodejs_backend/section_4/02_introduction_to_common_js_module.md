## Introduction to CommonJS Module System

In Node.js, the CommonJS module system is the standard way to organize and manage code. It allows developers to break their code into smaller, reusable pieces called modules. Each module can export its functionality, which can then be imported and used in other parts of the application.

### Exporting Modules
To export functionality from a module, you can use the `module.exports` object. This object is what gets returned when another module requires it. For example:

```javascript
// math.js
function add(a, b) {
    return a + b;
}
function subtract(a, b) {
    return a - b;
}
module.exports = {
    add,
    subtract
};
```
In this example, we have a `math.js` module that exports two functions: `add` and `subtract`. By assigning an object to `module.exports`, we can make these functions available to other modules.
### Importing Modules
To import a module, you can use the `require` function. This function takes the path to the module you want to import and returns the exported functionality. For example:

```javascript
// app.js
const math = require('./math');
const result = math.add(2, 3);
console.log(result); // Output: 5
```
In this example, we import the `math` module using `require('./math')`. We can then access the `add` function from the imported module and use it to perform an addition operation.
### Conclusion
The CommonJS module system is a powerful way to structure your Node.js applications. It promotes code reusability and maintainability by allowing you to break your code into smaller, manageable pieces. By using `module.exports` and `require`, you can easily share functionality across different parts of your application.