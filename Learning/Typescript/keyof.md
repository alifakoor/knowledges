اپراتور `Keyof` یک آبجکت دارای تایپ را دریافت می‌کند و یک رشته یا `Union` عددی از کلیدهای آن ایجاد می‌کند. در مثال زیر تایپ `P` همانند تایپ `"y" | "x"` است
```ts
type Point = { x: number; y: number };
type P = keyof Point;
```

```ts
type Arrayish = { [n: number]: unknown };
type A = keyof Arrayish; // در اینجا از نوع عدد است A تایپ 

type Mapish = { [k: string]: boolean };
type M = keyof Mapish; // در اینجا اجتماعی از تایپ های رشته و عدد است M تایپ
```

دقت کنید که در مثال بالا تایپ `M` از نوع `string | number` است. این به این خاطر است که کلیدها در آبجکت‌ها در زبان تایپ‌اسکریپت همواره مجبورند به رشته تبدیل شوند. بنابراین `obj[0]` همیشه با `obj["0"]` یکسان است.