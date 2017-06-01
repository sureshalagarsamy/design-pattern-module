# JavaScript design pattern(s)

JavaScript design patterns you should know

 * Module
 * Prototype
 * Observer
 * Singleton


### Module Design Pattern

Modules should be Immediately-Invoked-Function to allow for private scopes.This is what it looks like:

```javascript
(function() {
    // declare private variables and/or functions
    return {
      // declare public variables and/or functions
    }
})();
```

Here we instantiate the private variables and/or functions before returning our object that we want to return. Code outside of our closure is unable to access these private variables since it is not in the same scope. Let's take a more concrete implementation:

However, when outside the module, contents are unable to be referenced.

```javascript
var anonymousFunction = (function() {
  var privateVariable = 'ABCD'                  // private var
  var changePrivateFunction = function() {      // private function
  	//some code here
  }
  return {
    callChangeHTML: function() {
      changePrivateFunction();
      console.log(privateVariable);
    }
  };

})();

anonymousFunction.callChangeHTML();                 // Outputs: 'contents'
console.log(anonymousFunction.privateVariable);     // undefined
```

##### Revealing Module Pattern

The purpose is to maintain encapsulation and reveal certain variables and methods returned in an object literal.

```javascript
var Exposer = (function() {
  var privateVariable = 10;

  var privateMethod = function() {
    console.log('Inside a private method!');
    privateVariable++;
  }

  var methodToExpose = function() {
    console.log('This is a method I want to expose!');
  }

  var otherMethodIWantToExpose = function() {
    privateMethod();
  }

  return {
      first: methodToExpose,
      second: otherMethodIWantToExpose
  };
})();

Exposer.first();        // Output: This is a method I want to expose!
Exposer.second();       // Output: Inside a private method!
Exposer.methodToExpose; // undefined
```
