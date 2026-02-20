## Introduction to the FS Module

The `fs` module in Node.js provides an API for interacting with the file system. It allows you to read, write, and manipulate files and directories on your computer. The `fs` module is part of the core Node.js library, so you don't need to install it separately.

### Importing the FS Module
To use the `fs` module, you need to import it into your Node.js application.
```javascript
const fs = require('fs');
```

### Reading Files
You can read files using the `fs.readFile` method, which takes the file path and a callback function as arguments. The callback function will be called with an error (if any) and the data read from the file.
```javascript
fs.readFile('example.txt', 'utf8', (err, data) => {
    if (err) {
        console.error(err);
        return;
    }
    console.log(data);
});
```
### Writing Files
To write data to a file, you can use the `fs.writeFile` method. This method takes the file path, the data to write, and a callback function as arguments.
```javascript
const content = 'Hello, World!';
fs.writeFile('example.txt', content, (err) => {
    if (err) {
        console.error(err);
        return;
    }
    console.log('File has been written');
});
```
### Appending to Files
If you want to add content to an existing file without overwriting it, you can use the `fs.appendFile` method.
```javascript
const additionalContent = '\nThis is additional content.';
fs.appendFile('example.txt', additionalContent, (err) => {
    if (err) {
        console.error(err);
        return;
    }
    console.log('Content has been appended');
});
```
### Deleting Files
To delete a file, you can use the `fs.unlink` method, which takes the file path and a callback function as arguments.
```javascript
fs.unlink('example.txt', (err) => {
    if (err) {
        console.error(err);
        return;
    }
    console.log('File has been deleted');
});
```
### Conclusion
The `fs` module is a powerful tool for working with the file system in Node.js. It provides various methods for reading, writing, appending, and deleting files, allowing you to manage your files effectively. In the next sections, we will explore more advanced features of the `fs` module and how to use it in different scenarios.

### fs promises API

In addition to the callback-based API, the `fs` module also provides a promise-based API that allows you to use async/await syntax for better readability and error handling. You can access the promise-based API by using `fs.promises`.

```javascript
const fs = require('fs').promises;
async function readFileAsync() {
    try {
        const data = await fs.readFile('example.txt', 'utf8');
        console.log(data);
    } catch (err) {
        console.error(err);
    }
}
readFileAsync();
```

This allows you to write cleaner and more maintainable code when working with file operations in Node.js.