# Custom Find Method Polyfill

This is a simple polyfill for the `find` method in JavaScript arrays.

## Usage
To use the polyfill, include the following code snippet in your JavaScript file:

```javascript
if(!Array.prototype.myFind){
    Array.prototype.myFind = function(callback, thisArg){
        if(typeof callback !== 'function'){
            throw new TypeError(`${callback} must be function`)
        }
        if(this == null){
            throw new TypeError('myFind called on null data')
        }
        for(let i = 0; i<this.length;i++){
            if(callback.call(thisArg, this[i], i, this)){
                return this[i]
            }
        }
        return undefined;
    }
}


const numbers = [10, 20, 30, 40, 50];

const result = numbers.myFind((num) => num > 25);
console.log(result); 
// Output: 30

const users = [
  { name: "Alice", age: 25 },
  { name: "Bob", age: 30 },
  { name: "Charlie", age: 35 },
];

const foundUser = users.myFind((user) => user.name === "Bob");
console.log(foundUser); 
// Output: { name: 'Bob', age: 30 }
