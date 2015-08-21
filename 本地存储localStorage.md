#### localStorage

##### 存数据

```javascript
// 推荐使用setItem()方法保存数据
localStorage.setItem('myCat', 'Tom');

// 也可以这样保存数据
localStorage.myCat = 'Tom';

localStorage['myCat'] = 'Tom';
```

##### 取数据

```javascript
// 推荐使用getItem()方法取数据
var value = localStorage.getItem('myCat');

// 也可以这样
var value1 = localStorage.myCat;

var value2 = localStorage['myCat'];
```

##### 删除数据

```javascript
// 使用removeItem()方法删除数据
localStorage.removeItem('myCat');
```

##### 清空所有数据

```javascript
// 使用clear()方法清空所有本地存储数据
localStorage.clear();
```

##### 根据索引值获取key的name

```javascript
// 存储了一个数据myCat，它的索引为0，此时length=1
localStorage.setItem('myCat', 'Tom');
// 根据索引0取key的name
var keyname = localStorage.key(0);

console.log(keyname);   //'myCat'
```

##### 获取key的个数

```javascript
var len = localStorage.length;
```

##### 存储js对象

所有存储的值都被是字符串（如果存储的不是字符串也会默认转换为字符串形式），localStorage不支持存储其它类型的值，比如js对象。
如果想存储对象，需要做下转换，如下：

```javascript
var obj = {a: '1', b: '2', c: 'c'};
// 把js对象通过JSON.stringify转换为json字符串
localStorage.setItem('key', JSON.stringify(obj));

// 取数据
var jsonstr = localStorage.getItem('key');
// 把json字符串转化为js对象
var val = JSON.parse(jsonstr);
```

