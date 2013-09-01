
In brief:
- JavaScript does not have *block scope*, instead JavaScript uses **function scope**
- **Hoisting**. JavaScript’s function scope means that all variables declared within a function are visible *throughout* the body of the function
- Use **var** Inside Functions to Declare Variables, otherwise the variables will end up as global variables.


### Examples


---
// code from: David Flanagan@Mozilla - JavaScript, The Definitive Guide 6th Edition 

JavaScript does not have *block scope*, instead JavaScript uses **function scope:**
```javascript
function test(o) {	var i = 0; // i is defined throughout function	if (typeof o == "object") {		var j = 0; // j is defined everywhere, not just block		for(var k=0; k < 10; k++) { // k is defined everywhere, not just loop			console.log(k); // print numbers 0 through 9		}		console.log(k); // k is still defined: prints 10	}	console.log(j); // j is defined, but may not be initialized}
```
JavaScript’s function scope means that all variables declared within a function are visible*throughout* the body of the function, known as **hoisting**.
```javascript
var scope = "global";function f() {	console.log(scope); // Prints "undefined", not "global"	var scope = "local"; // Variable initialized here, but defined everywhere	console.log(scope); // Prints "local"}

// is equal to:

function f() {	var scope; // Local variable is declared at the top of the function	console.log(scope); // It exists here, but still has "undefined" value	scope = "local"; // Now we initialize it and give it a value	console.log(scope); // And here it has the value we expect}
```

---

Use **var** Inside Functions to Declare Variables and Avoid Scope Gotchas
```javascript
// case 1
// code from: Cody Lindley - JavaScript Enlightenment 
var foo = function() {	var boo = function() {		bar = 2; /* no var used, so bar is placed in the global scope at window.bar */	}();}();console.log(bar); // logs 2, because bar is in the global scope

// case 2, http://www.adequatelygood.com/JavaScript-Scoping-and-Hoisting.html
var foo = 1;
function bar() {
	if (!foo) {
		var foo = 10;
	}
	alert(foo);
}
bar(); // the answer is “10”
```
---