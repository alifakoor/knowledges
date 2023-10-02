![[function copy.jpg]]

در برنامه‌نویسی `functional` کد ما از ترکیب توابع محض (`pure functions`) و استفاده از داده‌های تغییرناپذیر (`immutable datas`) تشکیل شده است.

توابع محض: side effect ندارند، یعنی تاثیری روی متغیرهای خارج از محدوده خود ندارند، به ازای ورودی مشخص همیشه خروجی مشخص دارند.

داده‌های تغییرناپذیر، داده‌هایی هستند که پس از تعریف، ساختار آن‌ها تغییر نمی‌کند و هر تغییری، مانند افزودن یا حذف عنصر، داده‌ی جدیدی ایجاد می‌کند.
```ts
// روش تغییرپذیر(Mutable)
const firstTuple = [1,2];
firstTuple.push(3);
console.log(firstTuple); // [ 1, 2, 3]

// روش تغییرناپذیر(Immutable)
const secondTuple = [...firstTuple, 4];
console.log(secondTuple); // [1, 2, 3, 4]
console.log(firstTuple); // [1, 2, 3] 
```

-----------------

High Order Function (HOF)
![[65OD8kGW_t.jpg]]

----------------

## Memorization

در حقیقت هر بار با مقایسه ورودی‌ها متوجه می‌شویم که اگر ورودی یکسانی به تابع داده‌ایم، به جای این که یک‌ بار دیگر تابع را اجرا کنیم، خروجی تابع خود را در حافظه کش ذخیره می‌کنیم و مقدار درون حافظه را نمایش می‌دهیم.

```ts
function memorize<Input, Result>(fn: (input: Input) => Result) {
  const cacheMemory = new Map<Input, Result>()
  return function (input: Input): Result {
    if (cacheMemory.has(input)) return cacheMemory.get(input)!
    else {
      const result = fn(input)
      cacheMemory.set(input, result)
      return result
    }
  }
}

function add(a: number, b: number):number  {
  return a + b
}

const memorizedAdd = memorize((a: number) => memorize((b: number) => a + b))

memorizedAdd(5)(10)
```



