- Understand the difference between binding and assignment.
- **Key point** about closures: Closures store their outer variables by **reference**, *not* by value.

- lexical scoping: functions are executed using the variable scope that was in effect when they were defined, not the variable scope that is in effect when they are invoked.

- Currying. Partially applying functions.

- immediate function, (function(){})(), is incredibly versatile and ends up giving the JavaScript language a ton of unforeseen power. (Secret of JavaScript Ninja)


### Examples

---
// code from: David Flanagan@Mozilla - JavaScript Pocket Reference 3nd

**lexical scoping**
```javascript
var scope = "global scope"; // A global variable
function checkscope() {
	var scope = "local scope"; // A local variable
	function f() { return scope; }
	return f();
}
checkscope() // => "local scope"

var scope = "global scope"; // A global variable
function checkscope() {
	var scope = "local scope"; // A local variable
	function f() { return scope; }
	return f;
}
checkscope()() // What does this return? => "local scope"
```
---


---
// code from:David Herman@ Mozilla - Effective JavaScript - Item 11: Get Comfortable with Closures


```javascript
function sandwichMaker(magicIngredient) {
	function make(filling) {
		return magicIngredient + " and " + filling;
	}
	return make;
}
var hamAnd = sandwichMaker("ham");
hamAnd("cheese"); // "ham and cheese"
hamAnd("mustard"); // "ham and mustard"

var turkeyAnd = sandwichMaker("turkey");
turkeyAnd("Swiss"); // "turkey and Swiss"
turkeyAnd("Provolone"); // "turkey and Provolone"
```
---
---

Closures store their outer variables by **reference**, not by value.

// code from: David Herman@ Mozilla - Effective JavaScript - Item 13: Use Immediately Invoked Function Expressions to Create Local Scopes
```javascript
function wrapElements(a) {
	var result = [];
	for (i = 0, n = a.length; i < n; i++) {
		result[i] = function() { return a[i]; };
	}
	return result;
}
var wrapped = wrapElements([10, 20, 30, 40, 50]);
var f = wrapped[0];
f(); // undefined

// if we put the *var* declarations in the head of the for loop
function wrapElements(a) {
	var result = [];
	for (var i = 0, n = a.length; i < n; i++) {
		result[i] = function() { return a[i]; };
	}
	return result;
}
var wrapped = wrapElements([10, 20, 30, 40, 50]);
var f = wrapped[0];
f(); // undefined

// The solution is to force the creation of a local scope by creating a nested function and calling it right away:
function wrapElements(a) {
	var result = [];
	for (var i = 0, n = a.length; i < n; i++) {
		(function() {
			var j = i;
			result[i] = function() {
				return a[j];
			};
		})();
	}
	return result;
}
```

// code from: David Flanagan@Mozilla - JavaScript, The Definitive Guide 6th Edition -  8.6  Closures
```javascript
// case 1:
function constfunc(v) { // This function returns a function that always returns v
	return function() {
		return v;
	};
} 
var funcs = []; // Create an array of constant functions
for(var i = 0; i < 10; i++)
	funcs[i] = constfunc(i);
funcs[5]() // => 5 // The function at array element 5 returns the value 5.


// case 2:
function constfuncs() {
var funcs = [];
for(var i = 0; i < 10; i++)
	funcs[i] = function() { return i; };
	return funcs;
}
var funcs = constfuncs();
funcs[5]() // What does this return? => 10
funcs[8]() // => 10
// The code above creates 10 closures, and stores them in an array. The closures are all
defined within the same invocation of the function, so they *share* access to the variable
i.

// case 3:
// the code above only invoke constfuncs() once, yet here, we invoke couter() twice
// *each* invocation of counter() creates a *new* scope chain and a new private variable. So if you call counter() twice, you get two counter objects with different private variables.
function counter() {
	var n = 0;
	return {
		count: function() { return n++; },
		reset: function() { n = 0; }
	};
}
var c = counter(), d = counter(); // Create two counters
c.count() // => 0
d.count() // => 0: they count independently
c.reset() // reset() and count() methods share state
c.count() // => 0: because we reset c
d.count() // => 1: d was not reset
```

// code from: John Resig@jQuery - Secrets of the JavaScript Ninja - 5.6.2 Loops
```html
<body>
	<div>DIV 0</div>
	<div>DIV 1</div>
</body>
```
```javascript	
var divs = document.getElementsByTagName("div");
for (var i = 0; i < divs.length; i++) {
	divs[i].addEventListener("click", function() {
		alert("divs #" + i + " was clicked."); // The result: "div #2 is clicked". What's wrong?
	}, false);
}

// using an immediate function to solve
var div = document.getElementsByTagName("div");
for (var i = 0; i < div.length; i++) (function(n){
		div[n].addEventListener("click", function(){
		alert("div #" + n + " was clicked.");
	}, false);
})(i);
```
---
// Code from: Node.js in Action - 3.2 Asynchronous development challenges
```javascript
// without using closure
function asyncFunction(callback) {
	setTimeout(function() {
		callback()
	}, 200);
}
var color = 'blue';
asyncFunction(function() {
	console.log('The color is ' + color); // The result: 'green'
});
color = 'green';

// use closure
function asyncFunction(callback) {
	setTimeout(function() {
		callback()
	}, 200);
}
var color = 'blue';
(function(color) { // You immediately execute the anonymous function, sending it the current contents of color (as argument).
	asyncFunction(function() {
		console.log('The color is ' + color); // The result: 'blue'
	})
})(color);
color = 'green';
```
