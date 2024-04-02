## تایپ <Partial<Type[]

`Partial` تمام پراپرتی‌های یک تایپ را اختیاری می‌کند.

```ts
type User = {
  id: number;
  name: string;
};
let firstUser: User = {
  id: 1,
  name: "Quera",
}; // ✅

let secondUser: User = {
  name: "Quera",
}; // ❌ Property 'id' is missing in type '{ name: string; }' but required in type 'User'.

let partialUser : Partial<User>  = {
  name: "Quera",
}; // ✅
```


## تایپ <Required<Type[]

تایپ `Required` برخلاف `Partial` عمل می‌کند و تمام مقادیر را اجباری می‌کند
```ts
type User = {
  id?: number;
  name?: string;
};

let firstUser: User = {
  name: "Quera",
}; // ✅

let secondUser : Required<User> = {
  name: "Quera",
}; // ❌ Property 'id' is missing in type '{ name: string; }' but required in type 'Required<User>'.

let requiredUser : Required<User> = {
  id: 1,
  name: "Quera",
}; // ✅
```


## تایپ <Readonly<Type[]

`Readonly` همان‌طور که از نام آن مشخص است، یک اینترفیس یا تایپ را فقط خواندنی می‌کند و نمی‌توان هیچ تغییری در آن ایجاد کرد.

```ts
type User = {
  id: number;
  name: string;
};

let firstUser : Readonly<User> = {
  id: 1,
  name: "Quera",
};

firstUser.name = "college"; // ❌ Cannot assign to 'name' because it is a read-only property.
```


## تایپ <Record<Keys, Type[]

تایپ `Record` یکی از پرکاربردترین `Utility Type` ها است. `Record` دو تایپ را با هم ترکیب می‌کند. `Record` دو 
پارامتر دریافت می‌کند که پارامتر اول آن تایپ `key` ها و پارامتر دوم، تایپ `value` ها را مشخص می‌کند.
```ts
interface PageInfo {
title: string;
}

type Page = "home" | "about" | "contact";

const nav : Record<Page, PageInfo> = {
about: { title: "about" },
contact: { title: "contact" },
home: { title: "home" },
}; // ✅
```


## تایپ <Pick<Type, Keys[]

`Pick` یک تایپ شخصی‌سازی شده جدید بر اساس تایپ‌های موجود، ایجاد می‌کند.

```ts
type User = {
  id: number;
  name: string;
  age: number;
};

type UserName = Pick<User, "id" | "name">;

let pickUserName : UserName = {
  id: 1,
  name: "Quera",
}; // ✅

let secondUserName : UserName = {
  id: 1,
  name: "Quera",
  age: 20,
}; // ❌ Type '{ id: number; name: string; age: number; }' is not assignable to type 'UserName'.
//Object literal may only specify known properties, and 'age' does not exist in type 'UserName'.
```


## تایپ <Omit<Type, Keys[]

`Omit` یکی از پرکاربردترین `Utility Type` ها است. `Omit` مشابه `Pick` عمل می‌کند، یعنی یک تایپ شخصی‌سازی شده جدید بر اساس تایپ‌های موجود ایجاد می‌کند، با این تفاوت که پارامتر دوم، فیلدهایی هستند که می‌خواهیم در تایپ جدید وجود نداشته باشند.

```ts
type User = {
  id: number;
  name: string;
  age: number;
  lastActive: number;
};

type UserName = Omit<User, "id" | "name">;

let omitUserName : UserName = {
  age: 20,
  lastActive: 16302124725,
}; // ✅

let secondUserName : UserName = {
  name: "Quera",
  age: 20,
  lastActive: 16302124725,
}; // ❌ Type '{ name: string; age: number; lastActive: number; }' is not assignable to type 'UserName'.
//Object literal may only specify known properties, and 'name' does not exist in type 'UserName'.
```


## تایپ <Exclude<UnionType, ExcludedMembers

`Exclude` دو پارامتر ورودی دارد، پارامتر اول `Union Type` است و پارامتر دوم `Excluded Members`. `Exclude` مقادیر پارامتر دوم که با پارامتر اول یکسان هستند را حذف می‌کند.

```ts
type UnionType = "🍇" | "🍎" | "🍓" | "🍋";

let noApplesOrLemons : Exclude<UnionType, "🍋" | "🍎"> = "🍇"; // ✅ می‌تواند تایپ "🍇"|"🍓" داشته باشد.

let noLemons : Exclude<UnionType, "🍋"> = "🍋"; // ❌ Type '"🍋"' is not assignable to type '"🍇" | "🍎" | "🍓"'.
```


## تایپ <Extract<Type, Union[]

`Extract` به عنوان پارامتر اول تایپ مورد نظر را می‌گیرد و به عنوان پارامتر دوم تایپی که می‌خواهیم از تایپ اول استخراج کنیم را دریافت می‌کند.

```ts
type UnionType = "a" | "b" | "c";

type ExtractType = Extract<UnionType, "a" | "f">;

let extractVariable : ExtractType = "a"; // ✅

extractVariable = "c"; // ❌ Type '"c"' is not assignable to type '"a"'.

extractVariable = "f"; // ❌ Type '"f"' is not assignable to type '"a"'.
```


## تایپ <NonNullable<Type[]

از `NonNullable` برای حذف مقادیر `null` و `undefined` استفاده می‌کنیم.
```ts
type NonnullableType = string | number | null | undefined;

type NoNulls = NonNullable<NonnullableType>;

let noNullsVariable : NoNulls = "Quera"; // ✅

noNullsVariable = null; // ❌ Type 'null' is not assignable to type 'NoNulls'.
```


## تایپ <ReturnType<Type[]

با استفاده از `ReturnType`، تایپ خروجی تابع را مشخص می‌کنیم.
```ts
function sendData(a: number, b: number) {
  return {
    a: a,
    b: b,
  };
}

type RT1 = ReturnType<typeof sendData>; // ✅ {a:number, b:number}

type RT2 = ReturnType<any>; // ✅ any

type RT3 = ReturnType<never>; // ✅ never

type RT4 = ReturnType<() => string>; // ✅ string

type RT5 = ReturnType<(s: string) => void>; // ✅ void

type RT6 = ReturnType<<T>() => T>; // ✅ unknown

type RT7 = ReturnType<<T extends U, U extends number[]>() => T>; // ✅ number[]

type RT8 = ReturnType<string>; // ❌ Type 'string' does not satisfy the constraint '(...args: any) => any'.

type RT9 = ReturnType<Function>; // ❌ Type 'Function' does not satisfy the constraint '(...args: any) => any'.
//Type 'Function' provides no match for the signature '(...args: any): any'.
```


