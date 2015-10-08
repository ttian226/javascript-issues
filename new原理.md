
* 无论什么时候，只要创建一个新函数，就会根据一组特定的规则为该函数创建一个`prototype`属性，这个属性指向函数的原型对象。
* 在默认情况下，所有原型对象都会自动获得一个`constructor`（构造函数）属性，这个属性包含一个指向`prototype`属性所在函数的指针（就是指向新创建的函数）。
* 通过这个构造函数（原型对象的构造函数），可以继续为原型对象添加其他属性和方法。
* 当调用构造函数创建一个新实例后，该实例的内部将包含一个指针（内部属性），指向构造函数的原型对象。ECMA-262第5版管这个指针叫 [[Prototype]] 。脚本中没有标准的方式访问 [[Prototype]]，但Firefox、Safari和Chrome在每个对象上都支持一个属性__proto__；而在其他实现中，这个属性对脚本是完全不可见的。不过，要明确的真正重要的一点就是，这个连接存在于实例和构造函数的原型对象之间，而不是存在于实例和构造函数之间

#### new创建对象的步骤

1. 创建一个新的对象
2. 将构造函数的作用域赋给新对象
3. 执行构造函数的代码，为这个新对象添加属性
4. 返回新对象

```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.say = function () {
        console.log(this.name);
    };
}

function createPerson(P) {
    // 创建一个新对象
    var o = new Object();
    // 获取传递给Person函数的参数
    var args = Array.prototype.slice.call(arguments, 1);
    // 新对象的__proto__属性指向Person的原型对象
    o.__proto__ = P.prototype;
    // Person的原型对象的constructor指向Person
    P.prototype.constructor = P;
    // 把Person构造函数的作用域赋给新对象
    // 给这个新对象添加属性（name,age,say）
    P.apply(o, args);
    // 返回这个新对象
    return o;
}

var p = createPerson(Person, 'wang', 35);
```
