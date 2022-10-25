### Mapping Users to Get Usernames

In this question we are given an array of objects and asked to perfom these three tasks:

1. Write code to get array of names from given array of users
2. Get back only active users
3. Return users by age descending

```js
const users = [
    {
        id: 1,
        name: 'Jack',
        isActive: true,
        age: 20
    },
    {
        id: 1,
        name: 'John',
        isActive: true,
        age: 18
    },
    {
        id: 1,
        name: 'Mike',
        isActive: false,
        age: 30
    }
]
```

**Answer:**
```js
const names = users
    .sort((user1, user2) => (user1.age < user2.age ? 1: -1))
    .filter((user) => user.isActive)
    .map((user) => user.name);
```

This solution is better than using a for loop or a forEach function as it is cleaner and requires less operations. If we for instance needed to change something in our return array we would only need to refactor one line rather than potentially the entire loop.

*Functions Explained:* [sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort), [filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter), [map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

### Null vs Undefined ###

In this question we are given a two variables and asked what will be logged in each example

```js
let var1;
console.log(var1);
console.log(typeof var1);

  

let var2 = null;
console.log(var2);
console.log(typeof var2);
```

**Answer:**

```
undefined
undefined
null
object
```

The point to remember here is that `null` is not a type in JavsScript it is a value assigment . So when we console log a variable with a value of `null` it returns `Object` . 

`Undefined` however, means that this variable is declared but a value has not been declared yet inside this variable

### Hoisting in JS ###

In this question we are given two console logs and asked what will happen

```js
console.log(foo);
foo = 1;

console.log(foo);
var foo = 2;

foo = 3;
console.log(foo);
var foo;
```

**Answer:**

The first console log will return an `Uncaught Reference Error`, the second will return a value of 2, and the third a value of 3. This is due to the JS concept of [Hoisting] wherein function and variable definitions bubble to the top of the page. This concept does not apply however to `const` 's or `let` 's

### Closures in JS ###

In the following quesion we are given a function and ask what it logs to the console

```js
for (var i = 0; i < 3; i++) {
	const log = () => {
		console.log(i);
	}
	
	setTimeout(log, 100);
}
```

**Answer:**
``3,3,3

In this for loop the function `log()` is referencing the variable `i` which exists outside of its scope thereby creating a [[Closures|Closure]].  Because the variable `i` is a `var` its value is [[Hoisting|hoisted]] to the global scope upon definition. This means that after the loop has completed and the timeouts on the call stack exacute, the [[Closures|closure]] created by `log()` contains the final value of 3. However if instead of `var` the variable `i` was assigned by `let` we would see:

`0,1,2`

This is because variables defined by `let` are not [[Hoisting|hoisted]] meaning the scope of `i` is contained to the for loop. Because of this the [[Closures|closure]] is capturing the `log()` function a long with the variable `i` for each iteration of the loop. If we didnt have a [[Closures|closure]] here JavaScript would allocate that `i` variable in the [[Call Stack|call stack]] and then immediatley release it. Because *we do* have a [[Closures|closure]] it stores that variable in the [[Heap|heap memory]] so it can be referenced again when that [[Closures|closure]] is called by the timeout.

### Adding to the End of An Array

In this question we are asked to write a function which get's an array and an element and returns an array with this element at the end

```js
const numbers = [1, 2];
const append = (arr, el) => {
	// TRAP ANSWER:
	//arr.push(el);
	//return arr
	
	// Correct answer:
	return [...arr, el];
}

const newNumbers = append(numbers, 3);
console.log(newNumbers);
console.log(numbers);
```

The easiest answer here is to simply use `push()` to add the element to the end of the array however this is not best practice. Because `push()` mutates the given array instead of returning a new one you can run into a problem where you declare an array like `numbers` earlier in the code and later on execute the `append()` function and attempt to assign it to a new array thinking youre creating a new one. When in fact youve edited and returned `numbers`.

So instead of `push()` we should use the JS [[Spread Operator|spread operator]] to "spread" all of the elements of the given array onto a new copy and append the element to the end. This implementation is better because now `append()` is not modifying any data outside of itself but rather returning a new array. 
This combined with the fact that it will always return the same result given the same parameters means the function is [[Pure Functions|pure]].

> This same logic using the [[Spread Operator|spread operator]] can be [[Array and Object Destructuring#Object Destructuring|applied to objects]].

Similarly we may be asked to combine two arrays into one, instead of using the `push` function here it best to either use `concat` or the [[Spread Operator|spread operator]] like so:

```js
return [...arr1, ...arr2]
```

### Check if value exists in Array

In this question we are given an array of objects and asked to write a function that returns true if a given value exists in any of the objects. In this case a name.

```js
const arr = [
	{
		name: 'Jaime',
		id: 1
	},
	{
		name: 'Joe',
		id: 2
	},
	{
		name: 'Gracie',
		id: 3
	},
]

const isNameExists = (name, arr) => arr.some((el) => el.name === name);

const isNameExists2 = (name, arr) => {
	const index = arr.findIndex((el) => el.name === name);
	return index > 0;
}
```

The obvious answer is to simple solve this with a foor loop however JS provides us with some cleaner solutions shown above. The first uses the function [some()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some) which tests whether at least one element in the array passes the test implemented by the provided function. It returns true if, in the array, it finds an element for which the provided function returns true; otherwise it returns false.

The second best solution uses [findIndex()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex) which returns the index of the first element in an array that satisfies the provided testing function. If no elements satisfy the testing function, -1 is returned.

### Removing all Duplicates from an Array

In this question we are given an array of numbers and asked to remove all duplicates

```js
const uniqueArr = (arr) => {
	return [...new Set(arr)];
}

const uniqueArr2 = (arr) => {
	const result = [];
	arr.forEach((item) => {
		if(!result.includes(item)) {
			result.push(item);
		}
	});
	return result;
}
```

Here we have two viable solutions:

**Using a [Sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) object**
The [Sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set) object is a collection of values. A value in the `Set` **may only occur once**; it is unique in the `Set`'s collection. Because of this fact we can simply create a `new Set(arr)` and pass it the `arr`. Then use the [[Spread Operator|spread operator]] `...` to spread that set into an array and return it.


**Using [includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)**
If we loop through our array we can use [includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes) to check if the target array has a duplicate of the element we pass to [includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes). We can then simply push the current element if the array contains no duplicates of it.

