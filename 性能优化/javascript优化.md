#### 使用事件代理

如果你在一个div中有10个按钮，你只需要在div上附加一次事件句柄就可以了，而不用去为每一个按钮增加一个句柄。事件冒泡时你可以捕捉到事件并判断出是哪个事件发出的。

#### 缓存选择器查询结果

选择器查询是开销很大的方法。所以，使用选择器的次数应该越少越好，并且尽可能缓存选中的结果，便于以后反复使用。比如，下面这样的写法就是糟糕的写法:

```javascript
jQuery('#top').find('p.classA');
jQuery('#top').find('p.classB');
```

更好的写法是：

```javascript
var cached = jQuery('#top'); cached.find('p.classA'); cached.find('p.classB');
```

#### 避免频繁的IO操作

对 cookie 与 localstorage 操作的API是同步的，且cookie与localstorage是多个tab页面间共享的，多页面同时操作时会存在同步加锁机制，建议应尽量少的对cookie或localStorage进行操作。

#### 避免频繁的DOM操作

使用JavaScript访问DOM元素是比较慢的，因此为了提升性能，应该做到：
* 缓存已经查询过的元素；
* 线下更新完节点之后再将它们添加到文档树中；
* 避免使用JavaScript来修改页面布局；

原文[高性能javascript](http://www.alloyteam.com/2012/10/high-performance-front-end-high-performance-javascript/)
