# Custom indexOf Method Polyfill

This is a simple polyfill for the `indexOf` method in JavaScript arrays, without the `fromIndex` parameter.

## Usage

To use the polyfill, include the following code snippet in your JavaScript file:

```javascript
Array.prototype.myIndexOf = function(searchElement) {
    if (this == null) {
      throw new TypeError('Array.prototype.myIndexOf called on null or undefined');
    }

    var len = this.length >>> 0;

    for (var n = 0; n < len; n++) {
      if (n in this && this[n] === searchElement) {
        return n;
      }
    }
    return -1;
};


// Example array
var fruits = ['apple', 'banana', 'orange', 'banana', 'grape'];

// Using the myIndexOf method to find the index of 'banana'
var indexOfBanana = fruits.myIndexOf('banana');

console.log(indexOfBanana); // Output: 1

