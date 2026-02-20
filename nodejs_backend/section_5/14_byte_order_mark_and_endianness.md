## Byte Order Mark (BOM) and Endianness (Big Endian & Little Endian)

### Byte Order Mark (BOM)
- A Byte Order Mark (BOM) is a special marker at the beginning of a text file that indicates the encoding used in the file. It helps software to correctly interpret the text data.
- The BOM is typically represented as a sequence of bytes. For example, the UTF-8 BOM is represented as `EF BB BF` in hexadecimal.
- The presence of a BOM can help applications to automatically detect the encoding of a file, but it can also cause issues if not handled properly, especially in environments that do not expect it.
```javascript
// Example of a UTF-8 BOM in a text file
const fs = require('fs');
const data = fs.readFileSync('file_with_bom.txt');
console.log(data); // This will include the BOM bytes at the beginning
```

### Endianness (Big Endian & Little Endian)
- Endianness refers to the order of bytes in a multi-byte data type (like integers) when stored in memory or transmitted over a network.
- **Big Endian**: The most significant byte (MSB) is stored at the smallest memory address. For example, the number `0x12345678` would be stored as `12 34 56 78`.
- **Little Endian**: The least significant byte (LSB) is stored at the smallest memory address. For example, the number `0x12345678` would be stored as `78 56 34 12`.
```javascript
// Example of endianness in Node.js
const buffer = Buffer.alloc(4);
// Writing a number in Little Endian
buffer.writeUInt32LE(0x12345678, 0);
console.log(buffer); // Output: <Buffer 78 56 34 12>
// Writing a number in Big Endian
buffer.writeUInt32BE(0x12345678, 0);
console.log(buffer); // Output: <Buffer 12 34 56 78>
```
- Understanding endianness is crucial when working with binary data, especially when reading from or writing to files, or when communicating between different systems that may use different endianness.

- In Node.js, the `Buffer` class provides methods to read and write data in both big endian and little endian formats, allowing developers to handle endianness appropriately based on their needs.

