# Custom findIndex Method Polyfill

This is a simple polyfill for the `findIndex` method in JavaScript arrays.

## Usage

To use the polyfill, include the following code snippet in your JavaScript file:

```javascript
Array.prototype.myFindIndex = function(callback, thisArg) {
    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }
    
    for (var i = 0; i < this.length; i++) {
      if (callback.call(thisArg, this[i], i, this)) {
        return i;
      }
    }
    
    return -1;
};


// Example array
var numbers = [10, 20, 30, 40, 50];

// Using the myFindIndex method to find the index of the first number greater than 25
var indexOfFirstGreaterThan25 = numbers.myFindIndex(function(number) {
  return number > 25;
});

console.log(indexOfFirstGreaterThan25); // Output: 2
