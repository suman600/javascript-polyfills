# Custom map Polyfill

This is a simple polyfill for the `map` function in JavaScript arrays.

## Usage

To use the polyfill, simply include the following code snippet in your JavaScript file:

```javascript
if (!Array.prototype.myMap) {
    Array.prototype.myMap = function(callback, thisArg) {
        if (typeof callback !== "function") {
            throw new TypeError(`${callback} is not a function`);
        }
        let result = [];
        for (let i = 0; i < this.length; i++) {
            if (i in this) {
                result.push(callback.call(thisArg, this[i], i, this));
            }
        }
        return result;
    };
}



var numbers = [1, 2, 3, 4, 5];

function double(num) {
  return num * 2;
}

var doubledNumbers = numbers.myMap(double);

console.log(doubledNumbers); 
// Output: [2, 4, 6, 8, 10]