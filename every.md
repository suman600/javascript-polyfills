# Custom Every Method Polyfill

This is a simple polyfill for the `every` method in JavaScript arrays.

## Usage

To use the polyfill, include the following code snippet in your JavaScript file:

```javascript
Array.prototype.myEvery = function(callback, thisArg) {
    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }
    
    for (var i = 0; i < this.length; i++) {
      if (!callback.call(thisArg, this[i], i, this)) {
        return false;
      }
    }

    return true;
  };


// Example array
var numbers = [1, 2, 3, 4, 5];

// Using the myEvery method to check if all elements are greater than 0
var allGreaterThanZero = numbers.myEvery(function(num) {
  return num > 0;
});

console.log(allGreaterThanZero); // Output: true

