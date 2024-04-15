# Custom map Polyfill

This is a simple polyfill for the `map` function in JavaScript arrays.

## Usage

To use the polyfill, simply include the following code snippet in your JavaScript file:

```javascript
if (!Array.prototype.myMap) {
  Array.prototype.myMap = function(callback) {
    // Check if the callback is a function
    if (typeof callback !== 'function') {
      throw new TypeError('Callback must be a function');
    }

    var mappedArray = [];
    for (var i = 0; i < this.length; i++) {
      mappedArray.push(callback(this[i], i, this));
    }
    return mappedArray;
  };
}



// Example usage
var numbers = [1, 2, 3, 4, 5];

// Define a callback function to double each element
function double(num) {
  return num * 2;
}

// Use the polyfill myMap function to double each element of the array
var doubledNumbers = numbers.myMap(double);

console.log(doubledNumbers); // Output: [2, 4, 6, 8, 10]