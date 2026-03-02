## Write a function that takes a string a returns it reversed.
```javascript
function reverseString(str) {
    return str.split('').reverse().join('');
}
```

without using built-in functions:
```javascript
function reverseString(str) {
    let reversed = '';
    for (let i = str.length - 1; i >= 0; i--) {
        reversed += str[i];
    }
    return reversed;
}
```

## Write a function to check whether a given string is a palindrome.
```javascript
function isPalindrome(str) {
    const cleanedStr = str.replace(/[^A-Za-z0-9]/g, '').toLowerCase();
    const reversedStr = cleanedStr.split('').reverse().join('');
    return cleanedStr === reversedStr;
}
```
without using built-in functions:
```javascript
function isPalindrome(str) {
    let cleanedStr = '';
    for (let i = 0; i < str.length; i++) {
        const char = str[i];
        if (/[A-Za-z0-9]/.test(char)) {
            cleanedStr += char.toLowerCase();
        }
    }
    
    let reversedStr = '';
    for (let i = cleanedStr.length - 1; i >= 0; i--) {
        reversedStr += cleanedStr[i];
    }
    
    return cleanedStr === reversedStr;
}
```

## Write a function that returns the largest number from an array.
```javascript
function findLargestNumber(arr) {
    if (arr.length === 0) return null;
    let largest = arr[0];
    for (let i = 1; i < arr.length; i++) {
        if (arr[i] > largest) {
            largest = arr[i];
        }
    }
    return largest;
}
```

with built-in functions:
```javascript
function findLargestNumber(arr) {
    return Math.max(...arr);
}
```

## Write a function that removes duplicate values from an array.
```javascript
function removeDuplicates(arr) {
    const uniqueValues = [];
    for (let i = 0; i < arr.length; i++) {
        if (!uniqueValues.includes(arr[i])) {
            uniqueValues.push(arr[i]);
        }
    }
    return uniqueValues;
}
```
with built-in functions:
```javascriptfunction removeDuplicates(arr) {
    return [...new Set(arr)];
}
```

## Write a function that counts total vowels in a given string.
```javascript
function countVowels(str) {
    const vowels = 'aeiouAEIOU';
    let count = 0;
    for (let i = 0; i < str.length; i++) {
        if (vowels.includes(str[i])) {
            count++;
        }
    }
    return count;
}
```
without using built-in functions:
```javascript
function countVowels(str) {
    const vowels = 'aeiouAEIOU';
    let count = 0;
    for (let i = 0; i < str.length; i++) {
        for (let j = 0; j < vowels.length; j++) {
            if (str[i] === vowels[j]) {
                count++;
                break;
            }
        }
    }
    return count;
}
```

## Write a recursive function to calculate the factorial of a number.
```javascript
function factorial(n) {
    if (n === 0 || n === 1) {
        return 1;
    }
    return n * factorial(n - 1);
}
```
without using recursion:
```javascript
function factorial(n) {
    let result = 1;
    for (let i = 2; i <= n; i++) {
        result *= i;
    }
    return result;
}
```

## Write a function that checks whether a number is prime.
```javascript
function isPrime(num) {
    if (num <= 1) return false;
    for (let i = 2; i <= Math.sqrt(num); i++) {
        if (num % i === 0) return false;
    }
    return true;
}
```
without using built-in functions:
```javascript
function isPrime(num) {
    if (num <= 1) return false;
    for (let i = 2; i * i <= num; i++) {
        if (num % i === 0) return false;
    }
    return true;
}
```

## Write a function to find the second largest number in an array.
```javascript
function findSecondLargestNumber(arr) {
    if (arr.length < 2) return null;
    let largest = -Infinity;
    let secondLargest = -Infinity;
    
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] > largest) {
            secondLargest = largest;
            largest = arr[i];
        } else if (arr[i] > secondLargest && arr[i] !== largest) {
            secondLargest = arr[i];
        }
    }
    
    return secondLargest === -Infinity ? null : secondLargest;
}
```
with built-in functions:
```javascript
function findSecondLargestNumber(arr) {
    const uniqueNumbers = [...new Set(arr)];
    if (uniqueNumbers.length < 2) return null;
    uniqueNumbers.sort((a, b) => b - a);
    return uniqueNumbers[1];
}
```

## Write a function to flatten a deeply nested array.
```javascript
function flattenArray(arr) {
    const result = [];
    
    function flattenHelper(subArr) {
        for (let i = 0; i < subArr.length; i++) {
            if (Array.isArray(subArr[i])) {
                flattenHelper(subArr[i]);
            } else {
                result.push(subArr[i]);
            }
        }
    }
    
    flattenHelper(arr);
    return result;
}
```
with built-in functions:
```javascript
function flattenArray(arr) {
    return arr.flat(Infinity);
}
```

## Implement a debounce function in JavaScript.
```javascript
function debounce(func, delay) {
    let timeoutId;
    return function(...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => {
            func.apply(this, args);
        }, delay);
    };
}
```
without using built-in functions:
```javascript
function debounce(func, delay) {
    let timeoutId;
    return function() {
        const context = this;
        const args = arguments;
        clearTimeout(timeoutId);
        timeoutId = setTimeout(function() {
            func.apply(context, args);
        }, delay);
    };
}
```

## Write a function that returns the sum of all numbers in an array.
```javascript
function sumArray(arr) {
    return arr.reduce((sum, num) => sum + num, 0);
}
```
without using built-in functions:
```javascript
function sumArray(arr) {
    let sum = 0;
    for (let i = 0; i < arr.length; i++) {
        sum += arr[i];
    }
    return sum;
}
```

## Write a function to capitalize the first letter of every word in a string.
```javascript
function capitalizeFirstLetter(str) {
    return str.split(' ').map(word => word.charAt(0).toUpperCase() + word.slice(1)).join(' ');
}
```
without using built-in functions:
```javascript
function capitalizeFirstLetter(str) {
    let result = '';
    let capitalizeNext = true;
    
    for (let i = 0; i < str.length; i++) {
        if (str[i] === ' ') {
            result += ' ';
            capitalizeNext = true;
        } else if (capitalizeNext) {
            result += str[i].toUpperCase();
            capitalizeNext = false;
        } else {
            result += str[i];
        }
    }
    
    return result;
}
```

## Write a function to check whether two strings are anagrams.
```javascript
function areAnagrams(str1, str2) {
    const normalize = str => str.replace(/[^A-Za-z0-9]/g, '').toLowerCase().split('').sort().join('');
    return normalize(str1) === normalize(str2);
}
```
without using built-in functions:
```javascript
function areAnagrams(str1, str2) {
    function normalize(str) {
        let cleanedStr = '';
        for (let i = 0; i < str.length; i++) {
            const char = str[i];
            if (/[A-Za-z0-9]/.test(char)) {
                cleanedStr += char.toLowerCase();
            }
        }
        return cleanedStr.split('').sort().join('');
    }
    
    return normalize(str1) === normalize(str2);
}
```

## Given an array containing numbers from 1 to N with one number missing, find the missing number.
```javascript
function findMissingNumber(arr, N) {
    const expectedSum = (N * (N + 1)) / 2;
    const actualSum = arr.reduce((sum, num) => sum + num, 0);
    return expectedSum - actualSum;
}
```
without using built-in functions:
```javascript
function findMissingNumber(arr, N) {
    const expectedSum = (N * (N + 1)) / 2;
    let actualSum = 0;
    for (let i = 0; i < arr.length; i++) {
        actualSum += arr[i];
    }
    return expectedSum - actualSum;
}
```

## Write a function that counts the frequency of each character in a string.
```javascript
function countCharacterFrequency(str) {
    const frequency = {};
    for (let i = 0; i < str.length; i++) {
        const char = str[i];
        frequency[char] = (frequency[char] || 0) + 1;
    }
    return frequency;
}
```
without using built-in functions:
```javascript
function countCharacterFrequency(str) {
    const frequency = {};
    for (let i = 0; i < str.length; i++) {
        const char = str[i];
        if (frequency[char]) {
            frequency[char]++;
        } else {
            frequency[char] = 1;
        }
    }
    return frequency;
}
```

## Sort an array in ascending order without using the built-in .sort() method.
```javascript
function bubbleSort(arr) {
    const n = arr.length;
    for (let i = 0; i < n - 1; i++) {
        for (let j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j + 1]
                const temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    return arr;
}
```
with built-in functions:
```javascript
function sortArray(arr) {
    return arr.sort((a, b) => a - b);
}
```

## Write a function to check if two arrays are equal.
```javascript
function areArraysEqual(arr1, arr2) {
    if (arr1.length !== arr2.length) return false;
    for (let i = 0; i < arr1.length; i++) {
        if (arr1[i] !== arr2[i]) return false;
    }
    return true;
}
```
with built-in functions:
```javascript
function areArraysEqual(arr1, arr2) {
    return JSON.stringify(arr1) === JSON.stringify(arr2);
}
```

## Write a function to find common elements between two arrays.
```javascript
function findCommonElements(arr1, arr2) {
    const common = [];
    for (let i = 0; i < arr1.length; i++) {
        if (arr2.includes(arr1[i]) && !common.includes(arr1[i])) {
            common.push(arr1[i]);
        }
    }
    return common;
}
```
with built-in functions:
```javascript
function findCommonElements(arr1, arr2) {
    return arr1.filter(value => arr2.includes(value));
}
```

## Write a function to split an array into chunks of a given size.
```javascript
function chunkArray(arr, size) {
    const chunks = [];
    for (let i = 0; i < arr.length; i += size) {
        chunks.push(arr.slice(i, i + size));
    }
    return chunks;
}
```
without using built-in functions:
```javascript
function chunkArray(arr, size) {
    const chunks = [];
    for (let i = 0; i < arr.length; i += size) {
        const chunk = [];
        for (let j = i; j < i + size && j < arr.length; j++) {
            chunk.push(arr[j]);
        }
        chunks.push(chunk);
    }
    return chunks;
}
```

## Create your own implementation of JavaScript’s .map() method.
```javascript
function customMap(arr, callback) {
    const result = [];
    for (let i = 0; i < arr.length; i++) {
        result.push(callback(arr[i], i, arr));
    }
    return result;
}
```
without using built-in functions:
```javascript
function customMap(arr, callback) {
    const result = [];
    for (let i = 0; i < arr.length; i++) {
        result[i] = callback(arr[i], i, arr);
    }
    return result;
}
```

## Write a function that removes all falsy values (false, 0, “”, null, undefined, NaN) from an array.
```javascript
function removeFalsyValues(arr) {
    return arr.filter(Boolean);
}
```
without using built-in functions:
```javascript
function removeFalsyValues(arr) {
    const result = [];
    for (let i = 0; i < arr.length; i++) {
        if (arr[i]) {
            result.push(arr[i]);
        }
    }
    return result;
}
```

## Convert an array into an object using array values as keys and true as value.
```javascript
function arrayToObject(arr) {
    const obj = {};
    for (let i = 0; i < arr.length; i++) {
        obj[arr[i]] = true;
    }
    return obj;
}
```
without using built-in functions:
```javascript
function arrayToObject(arr) {
    const obj = {};
    for (let i = 0; i < arr.length; i++) {
        const key = arr[i];
        obj[key] = true;
    }
    return obj;
}
```

## Write a function to merge two objects without modifying the originals.
```javascript
function mergeObjects(obj1, obj2) {
    return { ...obj1, ...obj2 };
}
```
without using built-in functions:
```javascript
function mergeObjects(obj1, obj2) {
    const merged = {};
    for (let key in obj1) {
        if (obj1.hasOwnProperty(key)) {
            merged[key] = obj1[key];
        }
    }
    for (let key in obj2) {
        if (obj2.hasOwnProperty(key)) {
            merged[key] = obj2[key];
        }
    }
    return merged;
}
```

## Implement a function to deeply clone a nested object.
```javascript
function deepClone(obj) {
    if (obj === null || typeof obj !== 'object') {
        return obj;
    }
    
    if (Array.isArray(obj)) {
        return obj.map(item => deepClone(item));
    }
    
    const clonedObj = {};
    for (let key in obj) {
        if (obj.hasOwnProperty(key)) {
            clonedObj[key] = deepClone(obj[key]);
        }
    }
    return clonedObj;
}
```
without using built-in functions:
```javascript
function deepClone(obj) {
    if (obj === null || typeof obj !== 'object') {
        return obj;
    }
    
    if (Array.isArray(obj)) {
        const clonedArr = [];
        for (let i = 0; i < obj.length; i++) {
            clonedArr[i] = deepClone(obj[i]);
        }
        return clonedArr;
    }
    
    const clonedObj = {};
    for (let key in obj) {
        if (obj.hasOwnProperty(key)) {
            clonedObj[key] = deepClone(obj[key]);
        }
    }
    return clonedObj;
}
```

## Write a function that returns the longest word from a sentence.
```javascript
function findLongestWord(sentence) {
    const words = sentence.split(' ');
    let longestWord = '';
    
    for (let i = 0; i < words.length; i++) {
        if (words[i].length > longestWord.length) {
            longestWord = words[i];
        }
    }
    
    return longestWord;
}
```
without using built-in functions:
```javascript
function findLongestWord(sentence) {
    let longestWord = '';
    let currentWord = '';
    
    for (let i = 0; i < sentence.length; i++) {
        if (sentence[i] === ' ') {
            if (currentWord.length > longestWord.length) {
                longestWord = currentWord;
            }
            currentWord = '';
        } else {
            currentWord += sentence[i];
        }
    }
    
    // Check the last word
    if (currentWord.length > longestWord.length) {
        longestWord = currentWord;
    }
    
    return longestWord;
}
```

## Write a throttle function in JavaScript.
```javascript
function throttle(func, limit) {
    let lastFunc;
    let lastRan;
    return function() {
        const context = this;
        const args = arguments;
        if (!lastRan) {
            func.apply(context, args);
            lastRan = Date.now();
        } else {
            clearTimeout(lastFunc);
            lastFunc = setTimeout(function() {
                if ((Date.now() - lastRan) >= limit) {
                    func.apply(context, args);
                    lastRan = Date.now();
                }
            }, limit - (Date.now() - lastRan));
        }
    };
}
```
without using built-in functions:
```javascript
function throttle(func, limit) {
    let lastFunc;
    let lastRan;
    return function() {
        const context = this;
        const args = arguments;
        if (!lastRan) {
            func.apply(context, args);
            lastRan = new Date().getTime();
        } else {
            clearTimeout(lastFunc);
            lastFunc = setTimeout(function() {
                const now = new Date().getTime();
                if ((now - lastRan) >= limit) {
                    func.apply(context, args);
                    lastRan = now;
                }
            }, limit - (new Date().getTime() - lastRan));
        }
    };
}
```

## Write a function to check whether an object has no properties.
```javascript
function isEmptyObject(obj) {
    return Object.keys(obj).length === 0;
}
```
without using built-in functions:
```javascript
function isEmptyObject(obj) {
    for (let key in obj) {
        if (obj.hasOwnProperty(key)) {
            return false;
        }
    }
    return true;
}
```

## Convert a string like “hello world example” into “helloWorldExample”.
```javascript
function toCamelCase(str) {
    return str.split(' ').map((word, index) => {
        if (index === 0) {
            return word.toLowerCase();
        }
        return word.charAt(0).toUpperCase() + word.slice(1).toLowerCase();
    }).join('');
}
```
without using built-in functions:
```javascript
function toCamelCase(str) {
    let camelCaseStr = '';
    let capitalizeNext = false;
    
    for (let i = 0; i < str.length; i++) {
        if (str[i] === ' ') {
            capitalizeNext = true;
        } else {
            if (capitalizeNext) {
                camelCaseStr += str[i].toUpperCase();
                capitalizeNext = false;
            } else {
                camelCaseStr += str[i].toLowerCase();
            }
        }
    }
    
    return camelCaseStr;
}
```

## Group an array of objects by a given property.
Input: 
[
 {name: “A”, age:20},
 {name: “B”, age:20},
 {name: “C”, age:25}
]
Group by age
Output:
{
 20: [
   {name: “A”, age:20},
   {name: “B”, age:20}
 ],
 25: [
   {name: “C”, age:25}
 ]
}
```javascript
function groupBy(arr, property) {
    return arr.reduce((grouped, item) => {
        const key = item[property];
        if (!grouped[key]) {
            grouped[key] = [];
        }
        grouped[key].push(item);
        return grouped;
    }, {});
}
```
without using built-in functions:
```javascript
function groupBy(arr, property) {
    const grouped = {};
    for (let i = 0; i < arr.length; i++) {
        const key = arr[i][property];
        if (!grouped[key]) {
            grouped[key] = [];
        }
        grouped[key].push(arr[i]);
    }
    return grouped;
}
```

## Create your own implementation of Promise.all().
```javascript
function customPromiseAll(promises) {
    return new Promise((resolve, reject) => {
        const results = [];
        let completed = 0;
        
        promises.forEach((promise, index) => {
            Promise.resolve(promise)
                .then(result => {
                    results[index] = result;
                    completed++;
                    if (completed === promises.length) {
                        resolve(results);
                    }
                })
                .catch(error => {
                    reject(error);
                });
        });
    });
}
```
without using built-in functions:
```javascript
function customPromiseAll(promises) {
    return new Promise((resolve, reject) => {
        const results = [];
        let completed = 0;
        
        for (let i = 0; i < promises.length; i++) {
            (function(index) {
                Promise.resolve(promises[index])
                    .then(result => {
                        results[index] = result;
                        completed++;
                        if (completed === promises.length) {
                            resolve(results);
                        }
                    })
                    .catch(error => {
                        reject(error);
                    });
            })(i);
        }
    });
}
```

## Write a function that demonstrates closure behavior in JavaScript.
```javascript
function createCounter() {
    let count = 0;
    return function() {
        count++;
        return count;
    };
}
const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

## Create a function that runs only once, no matter how many times it is called.
```javascript
function runOnce(func) {
    let hasRun = false;
    return function() {
        if (!hasRun) {
            hasRun = true;
            return func.apply(this, arguments);
        }
    };
}
const initialize = runOnce(() => {
    console.log("Initialization complete.");
});
initialize(); // "Initialization complete."
initialize(); // No output
initialize(); // No output
```

## Convert a callback-based function into a Promise-based one.
```javascript
function callbackToPromise(func) {
    return function(...args) {
        return new Promise((resolve, reject) => {
            func(...args, (error, result) => {
                if (error) {
                    reject(error);
                } else {
                    resolve(result);
                }
            });
        });
    };
}
```
without using built-in functions:
```javascript
function callbackToPromise(func) {
    return function() {
        const args = Array.prototype.slice.call(arguments);
        return new Promise(function(resolve, reject) {
            args.push(function(error, result) {
                if (error) {
                    reject(error);
                } else {
                    resolve(result);
                }
            });
            func.apply(this, args);
        });
    };
}
```

## Write a function that retries a promise up to N times if it fails.
```javascript
function retryPromise(func, retries) {
    return new Promise((resolve, reject) => {
        function attempt() {
            func()
                .then(resolve)
                .catch(error => {
                    if (retries > 0) {
                        retries--;
                        attempt();
                    } else {
                        reject(error);
                    }
                });
        }
        attempt();
    });
}
```
without using built-in functions:
```javascript
function retryPromise(func, retries) {
    return new Promise(function(resolve, reject) {
        function attempt() {
            func()
                .then(resolve)
                .catch(function(error) {
                    if (retries > 0) {
                        retries--;
                        attempt();
                    } else {
                        reject(error);
                    }
                });
        }
        attempt();
    });
}
```

## Convert a nested object into a flat object.
{a: {b: {c:1}}} => {“a.b.c”:1}

```javascript
function flattenObject(obj, parentKey = '', result = {}) {
    for (let key in obj) {
        if (obj.hasOwnProperty(key)) {
            const newKey = parentKey ? `${parentKey}.${key}` : key;
            if (typeof obj[key] === 'object' && obj[key] !== null) {
                flattenObject(obj[key], newKey, result);
            } else {
                result[newKey] = obj[key];
            }
        }
    }
    return result;
}
```
without using built-in functions:
```javascript
function flattenObject(obj, parentKey, result) {
    parentKey = parentKey || '';
    result = result || {};
    
    for (let key in obj) {
        if (obj.hasOwnProperty(key)) {
            const newKey = parentKey ? parentKey + '.' + key : key;
            if (typeof obj[key] === 'object' && obj[key] !== null) {
                flattenObject(obj[key], newKey, result);
            } else {
                result[newKey] = obj[key];
            }
        }
    }
    return result;
}
```

## Return the first character in a string that does not repeat.
```javascript
function firstNonRepeatingCharacter(str) {
    const charCount = {};
    
    for (let i = 0; i < str.length; i++) {
        const char = str[i];
        charCount[char] = (charCount[char] || 0) + 1;
    }
    
    for (let i = 0; i < str.length; i++) {
        if (charCount[str[i]] === 1) {
            return str[i];
        }
    }
    
    return null;
}
```
without using built-in functions:
```javascript
function firstNonRepeatingCharacter(str) {
    const charCount = {};
    
    for (let i = 0; i < str.length; i++) {
        const char = str[i];
        if (charCount[char]) {
            charCount[char]++;
        } else {
            charCount[char] = 1;
        }
    }
    
    for (let i = 0; i < str.length; i++) {
        if (charCount[str[i]] === 1) {
            return str[i];
        }
    }
    
    return null;
}
```

## Create your own implementation of Array.prototype.filter.
```javascript
function customFilter(arr, callback) {
    const result = [];
    for (let i = 0; i < arr.length; i++) {
        if (callback(arr[i], i, arr)) {
            result.push(arr[i]);
        }
    }
    return result;
}
```
without using built-in functions:
```javascript
function customFilter(arr, callback) {
    const result = [];
    for (let i = 0; i < arr.length; i++) {
        if (callback(arr[i], i, arr)) {
            result[result.length] = arr[i];
        }
    }
    return result;
}
```

## Write a function to check deep equality of two objects.
```javascript
function deepEqual(obj1, obj2) {
    if (obj1 === obj2) return true;
    
    if (typeof obj1 !== 'object' || typeof obj2 !== 'object' || obj1 === null || obj2 === null) {
        return false;
    }
    
    const keys1 = Object.keys(obj1);
    const keys2 = Object.keys(obj2);
    
    if (keys1.length !== keys2.length) return false;
    
    for (let key of keys1) {
        if (!keys2.includes(key) || !deepEqual(obj1[key], obj2[key])) {
            return false;
        }
    }
    
    return true;
}
```
without using built-in functions:
```javascript
function deepEqual(obj1, obj2) {
    if (obj1 === obj2) return true;
    
    if (typeof obj1 !== 'object' || typeof obj2 !== 'object' || obj1 === null || obj2 === null) {
        return false;
    }
    
    const keys1 = [];
    for (let key in obj1) {
        if (obj1.hasOwnProperty(key)) {
            keys1.push(key);
        }
    }
    
    const keys2 = [];
    for (let key in obj2) {
        if (obj2.hasOwnProperty(key)) {
            keys2.push(key);
        }
    }
    
    if (keys1.length !== keys2.length) return false;
    
    for (let i = 0; i < keys1.length; i++) {
        const key = keys1[i];
        if (!keys2.includes(key) || !deepEqual(obj1[key], obj2[key])) {
            return false;
        }
    }
    
    return true;
}
```

## Implement a function that runs promises with a concurrency limit.
```javascript
function promisePool(functions, n) {
    return new Promise((resolve, reject) => {
        let i = 0;
        let active = 0;
        const results = [];
        
        function next() {
            if (i === functions.length && active === 0) {
                resolve(results);
                return;
            }
            
            while (active < n && i < functions.length) {
                const currentIndex = i;
                active++;
                functions[i++]()
                    .then(result => {
                        results[currentIndex] = result;
                        active--;
                        next();
                    })
                    .catch(error => {
                        reject(error);
                    });
            }
        }
        
        next();
    });
}
```
without using built-in functions:
```javascript
function promisePool(functions, n) {
    return new Promise(function(resolve, reject) {
        var i = 0;
        var active = 0;
        var results = [];
        
        function next() {
            if (i === functions.length && active === 0) {
                resolve(results);
                return;
            }
            
            while (active < n && i < functions.length) {
                (function(currentIndex) {
                    active++;
                    functions[i++]()
                        .then(function(result) {
                            results[currentIndex] = result;
                            active--;
                            next();
                        })
                        .catch(function(error) {
                            reject(error);
                        });
                })(i);
            }
        }
        
        next();
    });
}
```

## What will be the output of the following code and why?
console.log(“A”);
setTimeout(() => console.log(“B”), 0);
Promise.resolve().then(() => console.log(“C”));
console.log(“D”);
Output:
```
A
D
C
B
```
Explanation:
1. `console.log("A")` is executed first, so "A" is printed.
2. `setTimeout(() => console.log("B"), 0)` is called, which schedules "B" to be printed after the current call stack is cleared, but it will be placed in the task queue.
3. `Promise.resolve().then(() => console.log("C"))` is called, which schedules "C" to be printed after the current call stack is cleared, but it will be placed in the microtask queue, which has higher priority than the task queue.
4. `console.log("D")` is executed next, so "D" is printed.
5. After the current call stack is cleared, the microtask queue is processed first, so "C" is printed.
6. Finally, the task queue is processed, and "B" is printed.

## Create a sleep(ms) function that pauses execution using Promises.
```javascript
function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}
```
without using built-in functions:
```javascript
function sleep(ms) {
    return new Promise(function(resolve) {
        setTimeout(resolve, ms);
    });
}
```

## Write a function that memoizes another function’s results.
```javascript
function memoize(func) {
    const cache = {};
    return function(...args) {
        const key = JSON.stringify(args);
        if (cache[key]) {
            return cache[key];
        }
        const result = func.apply(this, args);
        cache[key] = result;
        return result;
    };
}
```
without using built-in functions:
```javascript
function memoize(func) {
    var cache = {};
    return function() {
        var args = Array.prototype.slice.call(arguments);
        var key = JSON.stringify(args);
        if (cache[key]) {
            return cache[key];
        }
        var result = func.apply(this, args);
        cache[key] = result;
        return result;
    };
}
```

## Convert a function f(a,b,c) into a curried version f(a)(b)(c).
```javascript
function curry(func) {
    return function curried(...args) {
        if (args.length >= func.length) {
            return func.apply(this, args);
        } else {
            return function(...nextArgs) {
                return curried.apply(this, args.concat(nextArgs));
            };
        }
    };
}
```
without using built-in functions:
```javascript
function curry(func) {
    return function curried() {
        var args = Array.prototype.slice.call(arguments);
        if (args.length >= func.length) {
            return func.apply(this, args);
        } else {
            return function() {
                var nextArgs = Array.prototype.slice.call(arguments);
                return curried.apply(this, args.concat(nextArgs));
            };
        }
    };
}
```

## Create your own implementation of Function.prototype.bind.
```javascript
function customBind(func, context, ...boundArgs) {
    return function(...args) {
        return func.apply(context, boundArgs.concat(args));
    };
}
```
without using built-in functions:
```javascript
function customBind(func, context) {
    var boundArgs = Array.prototype.slice.call(arguments, 2);
    return function() {
        var args = Array.prototype.slice.call(arguments);
        return func.apply(context, boundArgs.concat(args));
    };
}
```

## Write a function to detect circular references in an object.
```javascript
function hasCircularReference(obj, seen = new Set()) {
    if (obj && typeof obj === 'object') {
        if (seen.has(obj)) {
            return true;
        }
        seen.add(obj);
        for (let key in obj) {
            if (obj.hasOwnProperty(key)) {
                if (hasCircularReference(obj[key], seen)) {
                    return true;
                }
            }
        }
        seen.delete(obj);
    }
    return false;
}
```
without using built-in functions:
```javascript
function hasCircularReference(obj, seen) {
    seen = seen || [];
    if (obj && typeof obj === 'object') {
        if (seen.indexOf(obj) !== -1) {
            return true;
        }
        seen.push(obj);
        for (var key in obj) {
            if (obj.hasOwnProperty(key)) {
                if (hasCircularReference(obj[key], seen)) {
                    return true;
                }
            }
        }
        seen.pop();
    }
    return false;
}
```

## Convert:
[{id: 1, value: “A”}, {id: 2, value: “B”}]
into: 
{1: “A”, 2: “B”}

```javascript
function arrayToObject(arr) {
    const obj = {};
    for (let i = 0; i < arr.length; i++) {
        obj[arr[i].id] = arr[i].value;
    }
    return obj;
}
```
without using built-in functions:
```javascript
function arrayToObject(arr) {
    var obj = {};
    for (var i = 0; i < arr.length; i++) {
        obj[arr[i].id] = arr[i].value;
    }
    return obj;
}
```

## Create your own version of Promise.race().
```javascript
function customPromiseRace(promises) {
    return new Promise((resolve, reject) => {
        promises.forEach(promise => {
            Promise.resolve(promise)
                .then(resolve)
                .catch(reject);
        });
    });
}
```
without using built-in functions:
```javascript
function customPromiseRace(promises) {
    return new Promise(function(resolve, reject) {
        for (var i = 0; i < promises.length; i++) {
            Promise.resolve(promises[i])
                .then(resolve)
                .catch(reject);
        }
    });
}
```

## Implement a rate limiter that allows a function to be called only N times per second.
```javascript
function rateLimiter(func, limit) {
    let lastCalled = 0;
    return function(...args) {
        const now = Date.now();
        if (now - lastCalled >= 1000 / limit) {
            lastCalled = now;
            return func.apply(this, args);
        }
    };
}
```
without using built-in functions:
```javascript
function rateLimiter(func, limit) {
    var lastCalled = 0;
    return function() {
        var now = new Date().getTime();
        if (now - lastCalled >= 1000 / limit) {
            lastCalled = now;
            return func.apply(this, arguments);
        }
    };
}
```

## Implement a task queue that executes async tasks sequentially.
```javascript
class TaskQueue {
    constructor() {
        this.queue = [];
        this.isRunning = false;
    }
    
    add(task) {
        this.queue.push(task);
        this.run();
    }
    
    async run() {
        if (this.isRunning) return;
        this.isRunning = true;
        
        while (this.queue.length > 0) {
            const task = this.queue.shift();
            await task();
        }
        
        this.isRunning = false;
    }
}
```
without using built-in functions:
```javascript
function TaskQueue() {
    this.queue = [];
    this.isRunning = false;
}
TaskQueue.prototype.add = function(task) {
    this.queue.push(task);
    this.run();
};
TaskQueue.prototype.run = function() {
    var self = this;
    if (self.isRunning) return;
    self.isRunning = true;
    
    function next() {
        if (self.queue.length === 0) {
            self.isRunning = false;
            return;
        }
        var task = self.queue.shift();
        Promise.resolve(task()).then(next);
    }
    
    next();
};
```

## 



