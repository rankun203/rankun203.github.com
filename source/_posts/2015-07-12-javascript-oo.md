title: JavaScript OO
date: 2015-07-12 12:09:03
categories:
- programming
tags:
- javascript
---

ONE script to understand JavaScript OO :-)

```javascript
function MyClass () { // constructor function
  var privateVariable = "foo";  // Private variable 

  this.publicVariable = "bar";  // Public variable 

  this.privilegedMethod = function () {  // Public Method
    alert(privateVariable);
  };
}

// Instance method will be available to all instance but only load once in memory 
MyClass.prototype.publicMethod = function () {    
  alert(this.publicVariable);
};

// Static variable shared by all instance 
MyClass.staticProperty = "baz";

//...
var myInstance = new MyClass();
```

Clipped from StackOverflow: http://stackoverflow.com/a/1535687/1904043