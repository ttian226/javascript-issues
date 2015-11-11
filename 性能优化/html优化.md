#### 避免使用`<iframe>`

* 在页面加载过程中iframe元素会阻塞父文档onload事件的触发。
* 那是否有方案可以让onload事件不被iframe阻塞吗？有个简单的解决方案来避免onload事件被阻塞，使用JavaScript动态的加载iframe元素或动态设置iframe的src属性：(但其仅在高级浏览器 中有效，对于Internet Explorer 8及以下的浏览器无效。)

```html
<iframe id=iframe1 ></iframe>
 document.getElementById(‘iframe1’).setAttribute(‘src’， ‘url’);
```
* 除此之外我们必须知道iframe是文档内最消耗资源的元素之一，在Steve Souders 的测试中 ，在测试页面中分别加载100个A、DIV、SCRIPT、STYLE和 IFRAME元素，并且分别在Chrome、Firefox、Internet Explorer、Opera、Safari中运行了10次。结果显示创建iframe元素的开销比创建其他类型的DOM元素要高1~2个数量级。在测试中所有的DOM元素都是空的，如加载大的脚本或样式块可能比加载某些iframe元素耗时更长，但从基准测试结果来看，即使是空的iframe，其开销也是非常昂贵的，鉴于iframe的高开销，我们应尽量避免使用。尤其是对于移动设备，对于目前大部分还是只有有限的CPU与内存的情况下，更应避免使用iframe。


#### 避免空链接属性

空的链接属性是指img、link、script、ifrrame元素的src或href属性被设置了，但是属性却为空。如<img src=””>，我们创建了一个图片，并且暂时设置图片的地址为空，希望在未来动态的去修改它。但是即使图片的地址为空，浏览器依旧会以默认的规则去请求空地址

#### 避免节点深层级嵌套

深层级嵌套的节点在初始化构建时往往需要更多的内存占用，并且在遍历节点时也会更慢些，这与浏览器构建DOM文档的机制有关

#### 缩减HTML文档大小

#### 显式指定文档字符集

#### 显式设置图片的宽高

#### 避免脚本阻塞加载

当浏览器在解析常规的script标签时，它需要等待script下载完毕，再解析执行，而后续的HTML代码只能等待。为了避免阻塞加载，应把脚步放到文档的末尾，如把script标签插入在body结束标签之前

原文[高性能html](http://www.alloyteam.com/2012/10/high-performance-html/)
