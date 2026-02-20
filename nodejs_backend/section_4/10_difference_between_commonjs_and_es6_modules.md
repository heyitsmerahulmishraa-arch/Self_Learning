## Difference Between CommonJS and ES6 Modules

### CommonJS Modules
- CommonJS is a module system used in Node.js.
- It uses `require()` to import modules and `module.exports` to export them.
```javascript
// math.js
function add(a, b) {
    return a + b;
}
module.exports = { add };
// app.js
const math = require('./math');
console.log(math.add(2, 3)); // Output: 5
```

### ES6 Modules
- ES6 (ECMAScript 2015) introduced a standardized module system for JavaScript.
- It uses `import` to import modules and `export` to export them.
```javascript
// math.js
export function add(a, b) {
    return a + b;
}
// app.js
import { add } from './math.js';
console.log(add(2, 3)); // Output: 5
```

### Key Differences
1. **Syntax**: CommonJS uses `require()` and `module.exports`, while ES6 modules use `import` and `export`.
2. **Loading**: CommonJS modules are loaded synchronously, while ES6 modules are loaded asynchronously.
3. **Scope**: CommonJS modules have their own scope, while ES6 modules are scoped to the file they are defined in.
4. **Compatibility**: CommonJS is primarily used in Node.js, while ES6 modules are supported in both browsers and Node.js (with some configuration).
5. **Dynamic Imports**: ES6 modules support dynamic imports using `import()`, while CommonJS does not have built-in support for dynamic imports.
```javascript
// Dynamic import in ES6
import('./math.js').then(math => {
    console.log(math.add(2, 3)); // Output: 5
});
```

### Conclusion
Both CommonJS and ES6 modules have their own use cases and advantages. CommonJS is widely used in Node.js environments, while ES6 modules are the standard for modern JavaScript development and are supported in both browsers and Node.js. When working on new projects, it's generally recommended to use ES6 modules for better compatibility and future-proofing.

