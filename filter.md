# Custom Filter Polyfill

This is a simple polyfill for the `filter` method in JavaScript arrays.

## Usage

To use the polyfill, simply include the following code snippet in your JavaScript file:

```javascript
if (!Array.prototype.myFilter) {

    Array.prototype.myFilter = function(callback, thisArg) {
        if (typeof callback !== "function") {
            throw new TypeError(`${callback} is not a function`);
        }
        let result = [];
        for (let i = 0; i < this.length; i++) {
            if (i in this) {
                if (callback.call(thisArg, this[i], i, this)) {
                    result.push(this[i]);  // Add element if callback returns true
                }
            }
        }
        return result;
    };
}


// Example usage
var numbers = [1, 2, 3, 4, 5];

// Define a callback function to filter even numbers
function isEven(num) {
  return num % 2 === 0;
}

// Use the polyfill myFilter function to filter even numbers from the array
var evenNumbers = numbers.myFilter(isEven);

console.log(evenNumbers); // Output: [2, 4]
