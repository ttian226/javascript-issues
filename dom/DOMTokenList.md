#### [DOMTokenList](https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList)

The **DOMTokenList** interface represents a set of space-separated tokens. Such a set is returned by [Element.classList](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList), HTMLLinkElement.relList, HTMLAnchorElement.relList or HTMLAreaElement.relList. It is indexed beginning with 0 as with JavaScript Array objects. DOMTokenList is always case-sensitive

#### Properties

##### DOMTokenList.length

返回集合的长度

#### Methods

##### DOMTokenList.item()

根据索引返回指定的token

##### DOMTokenList.contains()

检查集合中是否存在指定的token

##### DOMTokenList.add()

给集合中添加一个token

##### DOMTokenList.remove()

在集合中删除一个token

##### DOMTokenList.toggle()

如果token存在则删除这个token返回false，如果token不存在则增加这个token返回true
