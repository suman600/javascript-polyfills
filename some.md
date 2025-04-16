# Custom Some Method Polyfill

This is a simple polyfill for the `some` method in JavaScript arrays.

## Usage

To use the polyfill, include the following code snippet in your JavaScript file:

```javascript
if (!Array.prototype.mySome) {
  Array.prototype.mySome = function(callback, thisArg) {
    if (typeof callback !== 'function') {
      throw new TypeError(`${callback} must be a function`);
    }

    if (this == null) {
      throw new TypeError('mySome called on null or undefined');
    }

    for (let i = 0; i < this.length; i++) {
      if (callback.call(thisArg, this[i], i, this)) {
        return true;
      }
    }

    return false;
  };
}

const numbers = [10, 21, 33, 44, 55];

const hasEven = numbers.mySome((num) => num % 2 === 0);
console.log(hasEven); // Output: true

const hasLargeNumber = numbers.mySome((num) => num > 100);
console.log(hasLargeNumber); // Output: false

const emptyArray = [];
const checkEmpty = emptyArray.mySome((x) => x > 0);
console.log(checkEmpty); // Output: false


