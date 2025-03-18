# Custom Apply Method Polyfill

This is a simple polyfill for the `apply` method in JavaScript arrays.

## Usage

To use the polyfill, include the following code snippet in your JavaScript file:

```javascript
if (!Function.prototype.myApply) {
  Function.prototype.myApply = function (context, thisArgs) {
    if (typeof this !== "function") {
      throw new TypeError(`${this} should be a function`);
    }
    if (thisArgs && !Array.isArray(thisArgs)) {
      throw new TypeError(`${thisArgs} should be an array`);
    }
    context = context || window;
    let funSymbol = Symbol();
    context[funSymbol] = this;
    const result = context[funSymbol](...(thisArgs || []));
    delete context[funSymbol];
    return result;
  };
}

// ✅ Test the polyfill
function logMessage(prefix, suffix) {
  console.log(`${prefix} ${this.name} ${suffix}`);
}

const user1 = { name: "Alice" };
const user2 = { name: "Bob" };

// ✅ Using the custom apply method
logMessage.myApply(user1, ["Hello,", "how are you?"]);
// Output: Hello, Alice how are you?

logMessage.myApply(user2, ["Hi,", "nice to meet you!"]);
// Output: Hi, Bob nice to meet you!

