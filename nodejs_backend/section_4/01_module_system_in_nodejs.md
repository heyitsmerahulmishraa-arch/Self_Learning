## Module System in Node.js

In Node.js, the module system is a fundamental part of how code is organized and reused. It allows developers to break their code into smaller, manageable pieces called modules. Each module can export its functionality, which can then be imported and used in other parts of the application.
### CommonJS Modules
The CommonJS module system is the original module system used in Node.js. It uses the `require` function to import modules and the `module.exports` object to export functionality.
```javascript
// math.js - A simple module that exports a function
function add(a, b) {
    return a + b;
}
module.exports = {
    add
};
```
```javascript
// app.js - Importing the math module
const math = require('./math');
const result = math.add(2, 3);
console.log(result); // Output: 5
```
### ES6 Modules
With the introduction of ES6, JavaScript now has a native module system. In Node.js, you can use ES6 modules by using the `.mjs` file extension or by setting `"type": "module"` in your `package.json` file.
```javascript
// math.mjs - A simple module that exports a function
export function add(a, b) {
    return a + b;
}
```
```javascript
// app.mjs - Importing the math module
import { add } from './math.mjs';
const result = add(2, 3);
console.log(result); // Output: 5
```
### Conclusion
The module system in Node.js is essential for organizing code and promoting code reuse. Whether you choose to use CommonJS or ES6 modules, understanding how to create and import modules is crucial for building scalable and maintainable applications in Node.js.

