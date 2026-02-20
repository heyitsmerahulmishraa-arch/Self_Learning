## Custom Require Function

In Node.js, the `require` function is used to import modules. However, you can also create your own custom `require` function if you want to implement specific behavior when loading modules. For example, you might want to add logging, handle errors differently, or implement a caching mechanism.
Here's an example of how you can create a custom `require` function:

```javascript
const Module = require('module');
const originalRequire = Module.prototype.require;

Module.prototype.require = function (moduleName) {
  console.log(`Requiring module: ${moduleName}`);
  return originalRequire.apply(this, arguments);
};
```
In this example, we are overriding the default `require` function by saving a reference to the original `require` function and then defining a new function that logs the name of the module being required before calling the original `require` function.
With this custom `require` function in place, every time you require a module, it will log the name of the module being loaded. For example:

```javascript
const fs = require('fs');
```
When you run this code, it will output:
```
Requiring module: fs
```
This allows you to add custom behavior to the module loading process while still maintaining the functionality of the original `require` function. You can further customize this function to suit your specific needs, such as adding error handling or implementing a caching mechanism for loaded modules.

In summary, creating a custom `require` function in Node.js allows you to modify the behavior of module loading, enabling you to add features such as logging, error handling, or caching while still retaining the core functionality of the original `require` function.

