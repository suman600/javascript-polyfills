# Custom Reduce Polyfill

This is a simple polyfill for the `reduce` method in JavaScript arrays.

## Usage

To use the polyfill, simply include the following code snippet in your JavaScript file:

```javascript
if (!Array.prototype.reduce) {
  Array.prototype.reduce = function(callback, initialValue) {
    // Check if the callback is a function
    if (typeof callback !== 'function') {
      throw new TypeError('Callback must be a function');
    }

    var accumulator = initialValue !== undefined ? initialValue : this[0];
    var startingIndex = initialValue !== undefined ? 0 : 1;

    for (var i = startingIndex; i < this.length; i++) {
      accumulator = callback(accumulator, this[i], i, this);
    }

    return accumulator;
  };
}


// Example usage
var numbers = [1, 2, 3, 4, 5];

// Define a callback function to sum all elements
function sumReducer(accumulator, currentValue) {
  return accumulator + currentValue;
}

// Use the polyfill reduce function to sum all elements of the array
var sum = numbers.reduce(sumReducer, 0);

console.log(sum); // Output: 15
