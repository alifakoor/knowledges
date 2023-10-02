```ts
function ruler(distance: number ,measurement:"cm" | "inch") {
 //... 
}

ruler(10,"cm");   // ✅
ruler(9,"inch");  // ✅
ruler(20,"kg");   // ❌
ruler(20,"ali");  // ❌

```

```ts
type Measurement= "cm"| "inch" | "mm";

function ruler(distance: number ,measurement:Measurement) {
    // ...
}

ruler(10,"cm"); // ✅ 
ruler(1,"kg");  // ❌!
```
