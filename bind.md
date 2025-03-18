# Custom Bind Method Polyfill

This is a simple polyfill for the `bind` method in JavaScript arrays.

## Usage

To use the polyfill, include the following code snippet in your JavaScript file:

```javascript
if (!Function.prototype.myBind) {
  Function.prototype.myBind = function (context, ...thisArgs) {
    if (typeof this !== "function") {
      throw new TypeError(`${this} should be a function`);
    }
    context = context || window;
    let funSymbol = Symbol();
    context[funSymbol] = this;
    return function (...newArgs) {
      const result = context[funSymbol](...thisArgs, ...newArgs);
      delete context[funSymbol];
      return result;
    };
  };
}

// ✅ Test function
function introduce(greeting, ending) {
  console.log(`${greeting}, I'm ${this.name} ${ending}`);
}

// ✅ Test object
const person = { name: "Charlie" };

// ✅ Test: Fully bind all arguments upfront
const boundIntroduce = introduce.myBind(person, "Hello", "Nice to meet you!");
boundIntroduce(); 
// Output: "Hello, I'm Charlie Nice to meet you!"

// ✅ Test: Partial bind with extra arguments later
const partiallyBoundIntroduce = introduce.myBind(person, "Hey");
partiallyBoundIntroduce("how's it going?");
// Output: "Hey, I'm Charlie how's it going?"
