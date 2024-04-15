# Custom includes Method Polyfill

This is a simple polyfill for the `includes` method in JavaScript arrays, without the `fromIndex` parameter.

## Usage

To use the polyfill, include the following code snippet in your JavaScript file:

```javascript
Array.prototype.myIncludes = function(searchElement) {
    if (this == null) {
      throw new TypeError('Array.prototype.myIncludes called on null or undefined');
    }

    for (var i = 0; i < this.length; i++) {
      if (this[i] === searchElement) {
        return true;
      }
    }

    return false;
};

// Example array
var fruits = ['apple', 'banana', 'orange', 'grape'];

// Using the myIncludes method to check if 'banana' is in the array
var includesBanana = fruits.myIncludes('banana');

console.log(includesBanana); // Output: true



