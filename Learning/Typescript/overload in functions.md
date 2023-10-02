هدف از `overload` کردن یک تابع این است که آن را چندین بار، به ازای انواع مختلف ورودی و انواع مختلف خروجی، استفاده کنیم.

```ts
type Values = string | number;
function sum(x: number, y: number): number;
function sum(x: string, y: string): string;
function sum(x: Values, y: Values) {
  if (typeof x === "string" || typeof y === "string") {
    return `${x} ${y}`;
  }
  return x + y;
}
const output1=sum(100,200);
const output2=sum("hi","sara");
output2.replaceAll('a','b') // ✅
```

نکات و قوانین `overload`

1. نام تابع و تعداد ورودی‌ها در تمامی`overload` ها باید یکسان باشد.
2. در هر`overload` نوع مناسب ورودی و خروجی مشخص شود.
3. `overload` قابلیت استفاده مجدد از کد را فراهم می‌کند، که باعث صرفه‌جویی در زمان و صرفه‌جویی در فضای حافظه می‌شود، به طوری که اجرای برنامه کمی سریعتر می‌شود.
4. این فرآیند همچنین خوانایی کد را افزایش می‌دهد.

