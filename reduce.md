# Custom Reduce Polyfill

This is a simple polyfill for the `reduce` method in JavaScript arrays.

## Usage

To use the polyfill, simply include the following code snippet in your JavaScript file:

```javascript
if(!Array.prototype.myReduce){
    Array.prototype.myReduce = function(callback, initialValue){
        if(!Array.isArray(this)){
            throw new TypeError(`${this} must be array`)
        }
        if(!typeof callback === 'function'){
            throw new TypeError(`callback must be function`)
        }
        let array = this;
        let accumulator = initialValue;
        let startIndex = 0;
        if(initialValue === undefined){
            if(array.length < 1){
                throw new TypeError('Empty array data')
            }
            initialValue = array[0];
            startIndex = 1;
        }
        for(let i = startIndex; i < array.length; i++){
            accumulator = callback(accumulator, array[i], i, array);
        }
        return accumulator;
    }
}
```

barebones version
```javascript
if (!Array.prototype.myReduce) {
  Array.prototype.myReduce = function (callback, initialValue) {
    let accumulator = initialValue !== undefined ? initialValue : this[0];
    let start = initialValue !== undefined ? 0 : 1;
    for (let i = start; i < this.length; i++) {
      accumulator = callback(accumulator, this[i], i, this);
    }

    return accumulator;
  };
}

// Test it out!
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.myReduce((acc, curr) => acc + curr, 0);

console.log(sum); // Output: 15

