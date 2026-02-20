## Module Wrapper Function

In Node.js, every module is wrapped in a function before it is executed. This is known as the "module wrapper function". The purpose of this wrapper function is to provide a private scope for the module's variables and functions, preventing them from polluting the global namespace.

The module wrapper function looks like this:

```javascript
(function (exports, require, module, __filename, __dirname) {
  // Module code goes here
});
```

When a module is loaded, Node.js wraps the module's code in this function and passes in the following parameters:
- `exports`: An object that the module can use to export its public API.
- `require`: A function that the module can use to import other modules.
- `module`: An object representing the current module, which has a `exports` property that can be used to export values.
- `__filename`: The absolute path of the current module file.
- `__dirname`: The absolute path of the directory containing the current module file.

This wrapper function allows each module to have its own scope, meaning that variables and functions defined in one module will not interfere with those in another module. It also provides a way for modules to export their functionality and import other modules as needed.

For example, if you have a module called `math.js` that exports a function to add two numbers, it might look like this:

```javascript
// math.js
function add(a, b) {
  return a + b;
}
module.exports = {
  add
};
```

When this module is loaded, Node.js will wrap it in the module wrapper function, allowing the `add` function to be exported and used in other modules without polluting the global namespace.

In summary, the module wrapper function is a fundamental part of how Node.js manages modules, providing a private scope for each module and enabling the export and import of functionality between modules.
