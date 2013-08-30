# This

## Reference
- Books
	- Cody Lindley - JavaScript Enlightenment - 6. The this Keyword
- Videos



### 



// Code from: "Cody Lindley - JavaScript Enlightenment"
```javascript<!DOCTYPE html><html lang="en"><body><script>var Person = function(name) {	this.name = name || 'john doe'; // this will refer to the instance created}var cody = new Person('Cody Lindley'); /* create an instance, based on Person constructor */console.log(cody.name); // logs 'Cody Lindley'</script></body></html>
```

**Had we not used the new keyword**, the value of this would be the context in which Person is invoked

```javascript
<!DOCTYPE html><html lang="en"><body><script>var Person = function(name) {	this.name = name || 'john doe';}var cody = Person('Cody Lindley'); // notice we did not use 'new'console.log(cody.name); // undefined, the value is actually set at window.name
console.log(window.name); // logs 'Cody Lindley'
</script></body></html>
```