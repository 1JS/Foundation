
- Understand the difference between binding and assignment.
- **Key point** about closures: Closures store their outer variables by **reference**, *not* by value.


### Examples

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
---
---
// code from: 
