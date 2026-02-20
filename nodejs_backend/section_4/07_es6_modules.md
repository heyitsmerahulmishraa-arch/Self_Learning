## ES6 Modules

ES6 Modules are a standardized way to organize and reuse code in JavaScript. They allow you to export functions, objects, or values from one file and import them into another file. This promotes modularity and helps keep your code organized.

### Exporting
To export a function, object, or value from a module, you can use the `export` keyword. There are two main ways to export: named exports and default exports.

#### Named Exports
```javascript
// math.js
export function add(a, b) {
    return a + b;
}
export function subtract(a, b) {
    return a - b;
}
```

#### Default Exports
```javascript
// math.js
export default function multiply(a, b) {
    return a * b;
}
```

### Importing
To import functions, objects, or values from a module, you can use the `import` keyword.

#### Importing Named Exports
```javascript
// main.js
import { add, subtract } from './math.js';
console.log(add(2, 3)); // Output: 5
console.log(subtract(5, 2)); // Output: 3
```

#### Importing Default Exports
```javascript
// main.js
import multiply from './math.js';
console.log(multiply(2, 3)); // Output: 6
```

### Conclusion
ES6 Modules provide a clean and efficient way to manage dependencies and organize code in JavaScript. They are widely supported in modern JavaScript environments and are an essential part of modern JavaScript development.
