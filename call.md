# Custom Call Method Polyfill

This is a simple polyfill for the `call` method in JavaScript arrays.

## Usage
To use the polyfill, include the following code snippet in your JavaScript file:

```javascript
if (!Function.prototype.myCall) {
  Function.prototype.myCall = function (context, ...thisArgs) {
    if (typeof this !== "function") {
      throw new TypeError(`${this} should be a function`);
    }
    context = context || window;
    let funSymbol = Symbol();
    context[funSymbol] = this;
    const result = context[funSymbol](...thisArgs);
    delete context[funSymbol];
    return result;
  };
}


function sayHello(greeting) {
  console.log(`${greeting}, ${this.name}`);
}

const user = { name: "Alice" };

sayHello.myCall(user, "Hello"); 
//  Output: "Hello, Alice"
