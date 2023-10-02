??
فقط زمانی که متغیر null, undefined نباشد اجرا شو
```ts
let speed: number | null = null;

let ride = {  
  // Nullish coalescing operator
  speed: speed ?? 30
}
```

```ts
 speed: speed !== null ? speed : 30
```

یعنی اگر speed = 0 باشد، مقدار صفر را قبول میکند، چون null یا undefined نیست