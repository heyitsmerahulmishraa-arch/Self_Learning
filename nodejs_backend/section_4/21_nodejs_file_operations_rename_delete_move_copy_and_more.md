## Node.js File Operations: Rename, Delete, Move, Copy, and More

In Node.js, you can perform various file operations such as renaming, deleting, moving, and copying files using the built-in `fs` module. Below are examples of how to perform these operations:
### 1. Renaming a File
To rename a file, you can use the `fs.rename()` method. This method takes the old path and the new path as arguments.

```javascript
const fs = require('fs');
const oldPath = 'oldFile.txt';
const newPath = 'newFile.txt';
fs.rename(oldPath, newPath, (err) => {
  if (err) throw err;
  console.log('File renamed successfully');
});
```
### 2. Deleting a File
To delete a file, you can use the `fs.unlink()` method. This method takes the path of the file to be deleted as an argument.

```javascript
const fs = require('fs');
const filePath = 'fileToDelete.txt';
fs.unlink(filePath, (err) => {
  if (err) throw err;
  console.log('File deleted successfully');
});
```
### 3. Moving a File
To move a file, you can use the `fs.rename()` method as well. Just specify the new path where you want to move the file.

```javascript
const fs = require('fs');
const oldPath = 'fileToMove.txt';
const newPath = 'newLocation/fileToMove.txt';
fs.rename(oldPath, newPath, (err) => {
  if (err) throw err;
  console.log('File moved successfully');
});
```
### 4. Copying a File
To copy a file, you can use the `fs.copyFile()` method. This method takes the source path and the destination path as arguments.

```javascript
const fs = require('fs');
const sourcePath = 'fileToCopy.txt';
const destinationPath = 'copyOfFile.txt';
fs.copyFile(sourcePath, destinationPath, (err) => {
  if (err) throw err;
  console.log('File copied successfully');
});
```

### 5. Checking if a File Exists
To check if a file exists, you can use the `fs.access()` method. This method takes the path of the file and a callback function as arguments.

```javascript
const fs = require('fs');
const filePath = 'fileToCheck.txt';
fs.access(filePath, fs.constants.F_OK, (err) => {
  if (err) {
    console.log('File does not exist');
  } else {
    console.log('File exists');
  }
});
```

### Conclusion
Node.js provides a powerful set of methods in the `fs` module to perform various file operations. Whether you need to rename, delete, move, or copy files, you can easily accomplish these tasks using the appropriate methods. Always remember to handle errors properly to ensure your application runs smoothly.

### with fs promise
In addition to the callback-based methods, Node.js also provides promise-based versions of these file operations using the `fs.promises` API. Here’s how you can perform the same operations using promises:

```javascript
const fs = require('fs').promises; 
// Renaming a file
async function renameFile(oldPath, newPath) {
  try {
    await fs.rename(oldPath, newPath);
    console.log('File renamed successfully');
  } catch (err) {
    console.error(err);
  }
}
// Deleting a file
async function deleteFile(filePath) {
  try {
    await fs.unlink(filePath);
    console.log('File deleted successfully');
  } catch (err) {
    console.error(err);
  }
}
// Moving a file
async function moveFile(oldPath, newPath) {
  try {
    await fs.rename(oldPath, newPath);
    console.log('File moved successfully');
  } catch (err) {
    console.error(err);
  }
}
// Copying a file
async function copyFile(sourcePath, destinationPath) {
  try {
    await fs.copyFile(sourcePath, destinationPath);
    console.log('File copied successfully');
  } catch (err) {
    console.error(err);
  }
}
// Checking if a file exists
async function checkFileExists(filePath) {
  try {
    await fs.access(filePath);
    console.log('File exists');
  } catch (err) {
    console.log('File does not exist');
  }
}
```
Using the promise-based API allows you to write cleaner and more readable code, especially when dealing with multiple asynchronous operations. You can also use `async/await` syntax to handle these operations in a more synchronous-like manner.

### Conclusion
Node.js provides both callback-based and promise-based APIs for file operations, giving you flexibility in how you handle asynchronous tasks. Whether you prefer callbacks or promises, you can easily perform file operations such as renaming, deleting, moving, and copying files in your Node.js applications. Always remember to handle errors properly to ensure your application runs smoothly.
