Javascript Closures are functions that can access values outside of their lexical scope[^1] . In order to call a function in your code the JS interpeter needs to know about the function itself and any surrounding data the function depends on.


![[Pasted image 20221018154646.png|300]]

When we look at a function that is fully self contained, and only relies on its own data we have a fully self contained, closed expression:

```js
function pureFun(a, b) {
	return a + b;
}
```

When its called its pushed onto the [[Call Stack|call stack]] where its executed and its internal data is only kept in memory until its popped back off the [[Call Stack|call stack]]. 

But when a function references data outside of its scope that gives an open expression that references other free variables throughout the enviroment

![[Pasted image 20221018155238.png|300]]

In order for the JS intrepreter to call this function and also know the value of these free variables it creates a Closure to store them in a place in memory where they can be accessed later. That memory is called the [[Heap|heap]] and unlike the [[Call Stack|call stack]] which is short lived it can keep memory indefinitely. Because of this closures use more memory and processing power than a typical function.

>So a closure is not just a function, its a function combined with its outer state or lexical enviroment

The most common use of closures is for data encapsulation[^2] 

```js
function outer() {
	let state = 'bunny';
	
	function inner() {
		return 'Hello ${state}';
	}
	
	return inner;
}
```

By defining an outer function that contains the state and an inner function that operates on it the data container here will not leak out to the surrounding enviroment. The `inner()` function has access to data defined in the `outer()` function's scope. But the `outer()` function does not have access to the `inner()` function


[^1]: In a programming language, an item's lexical scope is **the place in which it was created when it is created**.
[^2]: The mechanism whereby the data or state of an object is kept hidden to prevent leaking or exposing data where it is not needed

