```ts
function placeHolder <T> ( args : T[]): T[] {
return args;
}

let numPlaceHolder = placeHolder<number>([100, 200, 300]); // ✅

let strPlaceHolder = placeHolder<string>(["100", "200", "300"]); // ✅
```

از هر نام یا کاراکتری می‌توان به عنوان `Generic` استفاده کرد، ولی به طور معمول به دلیل تشابه آن با _Class Templates_ در _C++_ از `<T>` استفاده می‌شود.

می‌توانیم برای `Generic` ها چند مقدار در نظر بگیریم. به مثال زیر دقت کنید:
```ts

function multiGeneric<T, U>(id:T, name:U): U {

return name;

}

multiGeneric<number, string>(1, "Quera");
```

