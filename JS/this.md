# This


## Reference
- Books
	- Cody Lindley - JavaScript Enlightenment - 6. The this Keyword
- Videos




## About 'this'
The value of this, passed to all functions, is based on the **context** in which the function is called at **runtime (invoked)**.

- In ECMASript 3, The this Keyword Refers to the Head Object in Nested Functions. (fixed in ES5).
- The this Keyword Inside a Prototype Method Refers to a Constructor Instance.

### Examples

---
// 'this' in jQuery.
// code(tested) from: Jeffrey Way - 30 Days to Learn jQuery - 9.The-this-keyword

Since every jQuery selector, say $('.class'), is actually an instance of jQuery object, so…
```html
<a href="tutsplus.com">Click Me!</a>```
```javascript
// case 1
function doSomething(e) {
    console.log(this); // 'this' is: <a href="tutsplus.com">Click Me!</a>
	e.preventDefault();
}
$('a').on('click', doSomething);

// case 2
var obj = {
	doIt: function(e) {
		e.preventDefault();
		console.log(this); // 'this' is: <a href="tutsplus.com">Click Me!</a>
	}
}
$('a').on('click', obj.doIt);

// case 3
var obj = {
	doIt: function(e) {
		console.log(this); // 'this' is: obj
	}
}
$('a').on('click', function(e) {
	obj.doIt();
	e.preventDefault(); // since 'this' is not refer to the 'a' link, so we place the preventDefault code here.
});

// case 4
var obj = {
	doIt: function(e) {
		console.log(this); // 'this' is: <a href="tutsplus.com">Click Me!</a>
	}
}
$('a').on('click', function(e) {
	obj.doIt.call(this); // since here, 'this' is refer to the 'a' link
	e.preventDefault();
});

// case 5
var obj = {
	doIt: function(e) {
		console.log(this); // 'this' is: obj
		e.preventDefault();
	}
}
$('a').on( 'click', $.proxy(obj.doIt, obj) );
```
---
 
 
---
// 'this' in raw JavaScript
// code(tested) from: John Resig@jQuery - Secrets of the JavaScript Ninja
```html
<button id="test">Click Me!</button>``````javascriptvar button = {	clicked: false,	click: function(){
		console.log(this); // 'this' is: <button id="test">Click Me!</button>, not the 'button' object		this.clicked = true;	}};var elem = document.getElementById("test");elem.addEventListener("click",button.click,false); // the event handling system of the browser defines the context of the invocation to be the target element of the event, which causes the context to be the <button> element, not the button object.
```
---
 
 
---
// Code from: "Cody Lindley - JavaScript Enlightenment"

Use as constructor
```javascriptvar Person = function(name) {	this.name = name || 'john doe'; // this will refer to the instance created}var cody = new Person('Cody Lindley'); /* create an instance, based on Person constructor */console.log(cody.name); // logs 'Cody Lindley'
```

**Had we not used the new keyword**, the value of this would be the context in which Person is invoked

```javascript
var Person = function(name) {	this.name = name || 'john doe';}var cody = Person('Cody Lindley'); // notice we did not use 'new'console.log(cody.name); // undefined, the value is actually set at window.name
console.log(window.name); // logs 'Cody Lindley'
```
---
---
// code from: David Herman@Mozilla - Effective JavaScript

Invocation as a method
```javascript
var obj = {
	hello: function() {
		return "hello, " + this.username;
	},
	username: "Hans Gruber"
};
obj.hello(); // "hello, Hans Gruber", here 'this' is refer to the obj

var obj2 = {
	hello: obj.hello,
	username: "Boo Radley"
};
obj2.hello(); // "hello, Boo Radley, here 'this' is refer to obj2
```
---