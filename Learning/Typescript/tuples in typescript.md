tuples are like arrays but with constance length and item's type must be specified

e.g:
```ts
let firstTuple: [number, string] = [1, "hello"];
```

item's order is important in tuples

we can use `?` for make optional tuple's item
e.g:
```ts
let rgba: [number, number, number, number?];
rgba = [255, 0, 0]; // ✅
rgba = [255, 255, 0, 0.8]; // ✅
```

also we can use rest operator
e.g:
```ts
let secondTuple: [boolean, ...string[], number];
secondTuple = [true, "item1", "item2", "item3", 203]; // ✅
secondTuple = [true, 203]; // ✅
```



