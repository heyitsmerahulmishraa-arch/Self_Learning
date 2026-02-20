## Module Object

In Node.js, each file is treated as a separate module. When you require a module, Node.js wraps the code in that module in a function, which provides a private scope for the variables and functions defined within it. This means that variables and functions defined in one module are not accessible in another module unless they are explicitly exported.

### Exporting from a Module
To make variables, functions, or objects available to other modules, you can use the `module.exports` object. This is the object that will be returned when another module requires this module.
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
In the example above, we define two functions, `add` and `subtract`, and then export them as properties of the `module.exports` object. This allows other modules to access these functions when they require this module.

### Requiring a Module
To use the exported functions from another module, you can use the `require` function. This function takes the path to the module you want to import and returns the `module.exports` object from that module.
```javascript
// app.js
const math = require('./math');
console.log(math.add(5, 3)); // Output: 8
console.log(math.subtract(5, 3)); // Output: 2
```
In the example above, we require the `math` module and store the returned object in the `math` variable. We can then call the `add` and `subtract` functions that were exported from the `math` module.

