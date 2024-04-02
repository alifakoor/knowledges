enum stand for enumerations

در واقع `Enum`‌ ها ساختمان داده‌های نامرتبی در تایپ‌اسکریپت هستند که مانند آبجکت‌ها کلید (`key`) های ثابتی را به برخی مقادیر (`value` ) نگاشت می‌کنند.

two enum's type:
1. string to string: it means `key` and `value` are string
e.g:
```ts
enum Language {
 English = 'english',
 Spanish = 'spanish',
 Russian = 'russian'
}
```

2. string to number: it means `key` is string and `value` is number
e.g:
```ts
enum Language {
 English = 0,
 Spanish = 1,
 Russian = 2
}
```
if the values weren't specified, typescript default set from 0 to ...
e.g:
```ts
enum Language {
 English,
 Spanish,
 Russian
}
```

another example:
```ts
enum Language {
 English = 100,
 Spanish = 200 + 300,
 Russian // TypeScript infers 501 (the next number after 500)
}
```

__*combine two type together*__
```ts
enum Color {
 Red = '#c10000',
 Blue = '#007ac1',
 Pink = 0xc10050,
 White = 255 
}
```

__*important point*__
if use const before `enum` it not compiled to `js`

