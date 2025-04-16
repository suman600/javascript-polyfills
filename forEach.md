# Custom forEach Method Polyfill

This repository contains a simple polyfill for the `forEach` method in JavaScript.

## Usage
To use the polyfill, include the following code snippet in your JavaScript file:

```javascript
if (!Array.prototype.myForEach) {
    Array.prototype.myForEach = function (callback, thisArg) {
        if (typeof callback !== 'function') {
            throw new TypeError(`${callback} should be a function`);
        }
        
        for (let i = 0; i < this.length; i++) {
            if (this.hasOwnProperty(i)) {
                callback.call(thisArg, this[i], i, this);
            }
        }
    };
}


const numbers = [1, 2, 3, 4];

numbers.myForEach(function (item, i) {
    console.log(item + 10);
});
// Output:
//  11
//  12
//  13
//  14
```