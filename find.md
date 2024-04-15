# Custom Find Method Polyfill

This is a simple polyfill for the `find` method in JavaScript arrays.

## Usage

To use the polyfill, include the following code snippet in your JavaScript file:

```javascript
Array.prototype.myFind = function(callback, thisArg) {
    if (typeof callback !== 'function') {
      throw new TypeError(callback + ' is not a function');
    }
    
    for (var i = 0; i < this.length; i++) {
      if (callback.call(thisArg, this[i], i, this)) {
        return this[i];
      }
    }
    
    return undefined;
};


// Example array
var numbers = [1, 2, 3, 4, 5];

// Using the myFind method to find the first even number in the array
var firstEvenNumber = numbers.myFind(function(num) {
  return num % 2 === 0;
});

console.log(firstEvenNumber); // Output: 2
