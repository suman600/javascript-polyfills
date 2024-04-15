# Custom Filter Polyfill

This is a simple polyfill for the `filter` method in JavaScript arrays.

## Usage

To use the polyfill, simply include the following code snippet in your JavaScript file:

```javascript
if (!Array.prototype.myFilter) {
  Array.prototype.myFilter = function(callback) {
    // Check if the callback is a function
    if (typeof callback !== 'function') {
      throw new TypeError('Callback must be a function');
    }
    var filteredArray = [];
    for (var i = 0; i < this.length; i++) {
      if (callback(this[i], i, this)) {
        filteredArray.push(this[i]);
      }
    }
    return filteredArray;
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
