#### Properties of the Object constructor

##### Object.length

Has a value of 1

##### [Object.prototype](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype)

Allows the addition of properties to all objects of type Object.


#### Methods of the Object constructor


#### Object instances and Object prototype object


##### [Object.prototype.hasOwnProperty()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)

The **hasOwnProperty()** method returns a boolean indicating whether the object has the specified property.

`obj.hasOwnProperty(prop)`

* *prop* The name of the property to test

**Example1**

```javascript
var o = {
    val: '123',
    getVal: function() {
        return this.val;
    }
};

o.hasOwnProperty('val');        //true
o.hasOwnProperty('getVal');     //true
o.hasOwnProperty('toString');   //false
```

**Example2**

```javascript
// Iterator own's property
for (var name in o) {
    if (o.hasOwnProperty(name)) {
        // o[name]
    }
}
```

**Example3**

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.sayName = function() {
    return this.name;
};


var p = new Person('wangxu', 34);

p.hasOwnProperty('name');       //true
p.hasOwnProperty('sayName');    //false

Person.prototype.hasOwnProperty('name');    //false
Person.prototype.hasOwnProperty('sayName'); //true
```

##### [Object.prototype.isPrototypeOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/isPrototypeOf)

The **isPrototypeOf()** method tests for an object in another object's prototype chain

`prototypeObj.isPrototypeOf(obj)`
