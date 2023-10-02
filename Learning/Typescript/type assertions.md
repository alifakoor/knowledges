like `type casting` in Java

use `as`:
```ts

let x: any = "salam";

let y = x as string

console.log(typeof y) // output : string

```

use `<>` (angle-bracket):
```ts

let x: any = "salam";

let y = <string> x

console.log(typeof y) // output : string

```

