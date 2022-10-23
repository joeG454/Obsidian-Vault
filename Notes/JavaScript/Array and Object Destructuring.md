In ES6 we are given the ability to detructure iterables and manipulate them using the [[Spread Operator|spread operator]].

### Array Destructuring

Without destructuring if you wanted to log the first two elements of an array it may look something like this:

```js
const alphabet = ['A', 'B', 'C', 'D', 'E', 'F'];
const numbers = ['1', '2', '3', '4', '5', '6'];

const a = alphabet[0];
const b = alphabet[1];

console.log(a);
console.log(b);
```

However we can use destructuring to do this much cleaner:
```js
const [a, b] = alphabet;
```

The idea of destructring is you take the element you want to destructure and place it on the right side of the equal sign. On the left side we either use brackets `[]` for arrays or curly braces `{}`  for objects and within them we reference what elements we want to pull from the element on the right side of the equals. 

In the case of arrays the *position* of the elements determine what is pulled from the destructred array. So because `a` is in position 0 it pulls `alphabet[0]` and because `b` is in position 1 it pulls `alphabet[1]`

**Further Examples**:
```js
const [a, b, c] = alphabet
const [a,, c] = alphabet
const [a,, c, ..rest] = alphabet
```

 - The first example is an extension of the earlier one, creating three consts `a b c` each equal to `A B C` respectivley
 - The second example demonstrates that we can use commas to skip array elements, this creates two consts `a` and `c` each equal to `A` and `C` respectivley
 - The final example uses the [[Spread Operator|spread operator]] to create a const `rest` equal to the rest of the array that being `D E F`

Using the [[Spread Operator|spread operator]] we can also concat two arrays like so:
```js
const newArray = [...alphabet, ...numbers];
```

One of the most common uses of array destructuring is when youre dealing with functions and returning more than one parameter from a function.

```js
function sumAndMultiply(a, b) {
	return [a*b, a*b]
}

const [sum, multiply] = sumAndMultiply(2, 3)

console.log(sum) // RETURNS: 5
console.log(multiply) //RETURNS: 6
```

In this example `sumAndMultiply()` returns an array allowing us to destructure its response. In this way we can retrieve the sum and the muliply of the arguments separately. 

This also allows us to create default values like so:
```js
const [sum, multiply, division = 'No division'] = sumAndMultiply(2, 3)
console.log(division) // RETURNS: No Division
```

Because the reurn array of `sumAndMultiply()` has no third element we are getting the default value of `No division` . However, if we were to define that third value we would see:
```js
function sumAndMultiply(a, b) {
	return [a*b, a*b, a/b]
}

const [sum, multiply, division = 'No division'] = sumAndMultiply(2, 3)

console.log(division) //RETURN: 0.6666666666666666666666 
```

### Object Destructuring

```js
const personOne = {
	name: 'Joe',
	age: 27,
	address: {
		city: 'PHX',
		state: 'AZ'
	}
}

const personTwo = {
	name: 'Jaime',
	age: 26,
	address: {
		city: 'LA',
		state: 'CA'
	}
}

const {name, age} = personTwp
```