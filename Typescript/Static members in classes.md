در کلاس‌ها به پراپرتی‌هایی `Static` گفته می‌شود که بدون نیاز به اینکه نمونه‌ای از آن کلاس ساخته شود، بتوانیم به آن پراپرتی به صورت مستقیم دسترسی پیدا کنیم.

```ts
class Fruit {
  private name: string;
  private color: string;
  static maxRipeDays = 5;

  constructor(name: string, color: string) {
    this.name = name;
    this.color = color;
  }

  isRipe(): boolean {
    if (this.color === "green") {
      return false;
    } else {
      return true;
    }
  }
}

console.log(Fruit.maxRipeDays); // Output: 5
```

فرض کنید می‌خواهیم کلاسی تعریف کنیم که یکی از ویژگی‌هایی که دارد این است که تعداد سفارش‌های یک رستوران را به ما نمایش دهد. این کلاس را می‌توانیم به صورت زیر نمایش دهیم:
```ts
class Orders {
  ordersCount: number = 0;

  makeOrder = (): void => {
    this.ordersCount += 1;
  };
}

let order1 = new Orders();
order1.makeOrder();

let order2 = new Orders();
order2.makeOrder();

console.log(order1.ordersCount); // 1
console.log(order2.ordersCount); // 1
```

در مثال بالا یک کلاس به نام `Orders` ساختیم که یک پراپرتی به نام `ordersCount` دارد، که تعداد کل سفارشات را به ما نمایش می‌دهد و یک متد به نام `makeOrder` ساختیم که به تعداد سفارشات ما یک واحد اضافه می‌کند. بعد از انجام این کار، دو نمونه از این کلاس ساختیم و بوسیله هر کدام یکبار متد `makeOrder` را صدا زدیم. حال انتظار ما این است که مقدار سفارشات ما عدد `2` باشد اما زمانی که از `ordersCount` لاگ می‌گیریم مشاهده می‌کنیم که مقدار آن `1` است. چرا این اتفاق رخ داد؟ زیرا هر کدام از نمونه آبجکت‌هایی که ساختیم حافظه‌ی جداگانه‌ای را اشغال می‌کنند و به همین دلیل هر کدام از آبجکت‌هایی که تعریف کردیم پراپرتی `ordersCount` مخصوص به خود را دارند و چون برای هر کدام از آبجکت‌ها یکبار تابع `makeOrder` را صدا زدیم مقادیر `ordersCount` برابر `1` می‌باشد. اینجا ما نیاز داریم که بتوانیم پراپرتی تعریف کنیم که جایگاه ثابت در حافظه داشته باشد و با ساخت آبجکت‌های مختلف از کلاس به همان پراپرتی دسترسی داشته باشیم نه نمونه‌ای از آن. برای انجام اینکار باید از کلیدواژه `static` قبل از پراپرتی مورد نظر استفاده کنیم. به مثال زیر توجه کنید:

```ts
class Orders {
  private static _ordersCount: number = 0;

  makeOrder(): void {
    Orders._ordersCount += 1;
  }

  get ordersCount() {
    return Orders._ordersCount;
  }
}

let order1 = new Orders();
order1.makeOrder();

let order2 = new Orders();
order2.makeOrder();

console.log(order1.ordersCount); // 2
```

در مثال بالا متغیر `ordersCount` را به صورت `Static` تعریف کردیم و اینگونه توانستیم به صورت مستقیم به پراپرتی `ordersCount` دسترسی داشته باشیم و پراپرتی با مقدار ثابت در حافظه تعریف کنیم. حال زمانی که دوبار متد `makeOrder` را صدا می‌زنیم مقدار `ordersCount` برابر `2` می‌شود.