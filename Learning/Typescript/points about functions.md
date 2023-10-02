
for making an input optional in function, you can just add `?` to end of it
e.g:

```ts
const addTwoNumbers = 
(a: number, b: number, convertToHexadecimal?: boolean): number | string => {
	const sum = a + b;
	if (convertToHexadecimal) {
		const hexString = sum.toString(16);
		return hexString;
	}
	return sum;
};

console.log(addTwoNumbers(1, 10)); // => 11 ✅
console.log(addTwoNumbers(1, 10, true)); // => 'b' ✅
```
----

just `null` and `undefined` value are acceptable in `void` type
e.g:

```ts
const addTwoNumbers = (a: number, b: number): void => {
	console.log(a + b)
};

addTwoNumbers(2,4) // return undefined and log 6 on console.
```
----

rest operator in function's input
e.g:

```ts
const addNumbers = (...numbers: number[]): number => {
	return numbers.reduce((prev, current)=>{
		return prev + current;
	}, 0)
};

console.log(addNumbers(2, 4, 5, 7)); // return 18
```
----

