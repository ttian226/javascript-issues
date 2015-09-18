#### [History](https://developer.mozilla.org/en-US/docs/Web/API/History)

方法

history.pushState(state, title, url);

* state它可以理解为一个拿来存储自定义数据的元素。它和同时作为参数的url会关联在一起。
* title是一个字符串，目前各类浏览器都会忽略它（以后才有可能启用，用作页面标题），所以设置成什么都没关系。目前建议设置为空字符串。
* url是url地址

关于url，假设页面url地址是`http://localhost:63342/dom/history.html`

    1.如果url='/1',地址变为http://localhost:63342/1
    2.如果url='1',地址变为http://localhost:63342/dom/1
    3.如果url='?1',http://localhost:63342/dom/history.html?1
    4.如果url='#1',http://localhost:63342/dom/history.html#1

例子：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title></title>
    <link rel="stylesheet" href="demo.css"/>
</head>
<body>
<title>HTML5 History API</title>
<style>
    #examples {
        padding-left: 20px;
    }
    #examples li {
        list-style: square;
        padding: 0;
        margin: 0;
    }
</style>
<article>
    <p id="status">HTML5 History API not supported</p>
    <p><em>Last event fired: <span id="lastevent">(none)</span></em></p>
    <p>To test the History API, click through the urls below. Note that none of these urls point to <em>real</em> pages. JavaScript will intercept these clicks, load data and the browser address bar will <em>appear</em> to change - but this is the History API in action!</p>
    <p>Use the back and forward buttons in your browser to navigate the history.</p>
    <ul id="examples">
        <li><a href="/history/first">first</a></li>
        <li><a href="/history/second">second</a></li>
        <li><a href="/history/third">third</a></li>
        <li><a href="/history/fourth">fourth</a></li>
    </ul>
    <p><small>Note: since these urls aren't real, refreshing the page will land on an invalid url.</small></p>
    <div id="output"></div>
</article>
</body>
<script src="his.js"></script>
</html>
```

```javascript
var $ = function (id) {
        return document.getElementById(id);
    },
    state = $('status'),
    lastevent = $('lastevent'),
    examples = $('examples'),
    output = $('output'),
    template = '<p>URL: <strong>{url}</strong>, name: <strong>{name}</strong>, location: <strong>{location}</strong></p>',
    
    // 假设data是ajax请求的数据
    data = {
        first : {
            name: "Remy",
            location: "Brighton, UK"
        },
        second: {
            name: "John",
            location: "San Francisco, USA"
        },
        third: {
            name: "Jeff",
            location: "Vancover, Canada"
        },
        fourth: {
            name: "Simon",
            location: "London, UK"
        }
    };


// 判断history api是否可用
if (typeof history === 'undefined') {
    state.className = 'fail';
} else {
    state.className = 'success';
    state.innerHTML = 'HTML5 History API available';
}

// 点击事件
examples.addEventListener('click', function (e) {
    var title;
    e.preventDefault();
    if (e.target.nodeName.toLowerCase() === 'a') {
        title = e.target.innerHTML;
        data[title].url = e.target.getAttribute('href');
        var url = e.target.href;    //获取a标签链接
        history.pushState(data[title], title, url);
        reportData(data[title]);
    }
}, false);

// 当有history.pushState数据时，并且点击浏览器的后退或前进按钮会触发popstate事件
window.addEventListener('popstate', function (e) {
    var data = e.state;
    reportEvent(e);
    reportData(data || { url: "unknown", name: "undefined", location: "undefined" });
}, false);

// 记录当前data数据
function reportData(data) {
    output.innerHTML = template.replace(/(\{(.*?)\})/g, function (a,b,c) {
        return data[c];
    });
}

// 记录事件类型
function reportEvent(e) {
    lastevent.innerHTML = e.type;
}
```
