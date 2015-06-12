

##### document.getElementById(id)
Returns a reference to the element by its ID.
* element is a reference to an **Element** object, or null if an element with the specified ID is not in the documen
* id is a case-sensitive string representing the unique ID of the element being sought

##### document.getElementsByTagName(name)
Returns an **HTMLCollection** of elements with the given tag name.


##### document.querySelector(selectors)
Returns the first element within the document (using depth-first pre-order traversal of the document's nodes) that matches the specified group of selectors.

```javascript
var element = document.querySelector(selectors);
```
* **element** is an element object.
* **selectors** is a string containing one or more CSS selectors separated by commas

##### document.querySelectorAll(selectors)
Returns a list of the elements within the document (using depth-first pre-order traversal of the document's nodes) that match the specified group of selectors. The object returned is a **NodeList**.