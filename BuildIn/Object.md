#### Properties of the Object constructor

##### Object.length

Has a value of 1

##### [Object.prototype](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/prototype)

Allows the addition of properties to all objects of type Object.


#### Methods of the Object constructor

##### [Object.create()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create)

用指定的原型对象创建一个新的原型对象

```javascript
function Shape() {
    this.x = 0;
    this.y = 0;
}
// 原型方法move
Shape.prototype.move = function(x, y) {
    this.x += x;
    this.y += y;
    console.info('Shape moved.');
};
function Rectangle() {
    Shape.call(this); //调用Shape的构造函数，此时Rectangle也有两个属性x,y
}
// 用Shape的原型对象初始化Rectangle的原型对象，此时Rectangle继承了Shape的原型方法move
Rectangle.prototype = Object.create(Shape.prototype);
Rectangle.prototype.constructor = Rectangle;
// 创建Rectangle的实例r
var r = new Rectangle();
// 调用原型方法move
r.move(10, 20);
```

##### [Object.keys()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)

返回对象可枚举的属性集合（不包括继承属性）

```javascript
var arr = ['a', 'b', 'c'];
console.log(Object.keys(arr)); // console: ['0', '1', '2']

// array like object
var obj = { 0: 'a', 1: 'b', 2: 'c' };
console.log(Object.keys(obj)); // console: ['0', '1', '2']

// array like object with random key ordering
var an_obj = { 100: 'a', 2: 'b', 7: 'c' };
console.log(Object.keys(an_obj)); // console: ['2', '7', '100']
```

##### [Object.defineProperty()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty)

##### [Object.defineProperties()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperties)

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

* *prototypeObj* An object to be tested against each link in the prototype chain of the object argument.
* *obj* The object whose prototype chain will be searched. 

**Example**

```javascript
function Rectangle() {

}

var rec = new Rectangle();

Rectangle.prototype.isPrototypeOf(rec); //true
```

##### [Object.prototype.toString()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/toString)

The **toString()** method returns a string representing object.

**Example:** Using toString() to detect object class

```javascript
var toString = Object.prototype.toString;

toString.call(new Date);    // [object Date]
toString.call(new String);  // [object String]
toString.call(Math);        // [object Math]
```
##### [Object.prototype.valueOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf)

The **valueOf()** method returns the primitive value of the specified object.

Some difference from `toString` and `valueOf`:

```javascript
var o = {
    str: 'hello',
    val: 10,
    toString: function() {
        return this.str;
    },
    valueOf: function() {
        return this.val;
    }
};

// o.toString()
alert(o);   //'hello'
var str = ['abc', o].join(','); 
alert(str); //'abc,hello'

// o.valueOf()
alert("o=" + o);    //'o=10'
alert('20' + o);    //'2010'
alert(20 + o);      //30
```
