#### [DOMTokenList](https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList)

The **DOMTokenList** interface represents a set of space-separated tokens. Such a set is returned by [Element.classList](https://developer.mozilla.org/en-US/docs/Web/API/Element/classList), HTMLLinkElement.relList, HTMLAnchorElement.relList or HTMLAreaElement.relList. It is indexed beginning with 0 as with JavaScript Array objects. DOMTokenList is always case-sensitive

#### Properties

##### DOMTokenList.length

Is an integer representing the number of objects stored in the object.

#### Methods

##### DOMTokenList.item()

Returns an item in the list by its index

##### DOMTokenList.contains()

Returns true if the underlying string contains token, otherwise false

##### DOMTokenList.add()

Adds token to the underlying string

##### DOMTokenList.remove()

Removes token from the underlying string

##### DOMTokenList.toggle()

Removes token from string and returns false. If token doesn't exist it's added and the function returns true
