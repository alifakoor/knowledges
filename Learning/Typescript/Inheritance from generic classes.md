بطور کلی ۳ روش برای extend کردن از یک generic class وجود دارد
## پاس دادن ورودی جنریک تایپ‌ها به واسطه‌ی کلاس فرزند
```ts
  class CompressibleStore<T> extends Store<T> {
    compress() {
      // compressing process...
    }
  }
```

## محدود کردن ورودی جنریک تایپ‌ها
```ts
class SearchableStore<T extends { name: string }> extends Store<T> {
    find(name: string): T | undefined {
      return this._objects.find((obj) => obj.name === name);
    }
  }
```
در مثال بالا با `extend` کردن ورودی تایپ جنریک `T` از شیء `{ name: string}` به تایپ‌اسکریپت می‌فهمانیم که انتظار داریم هر تایپ وروردی که به عنوان جنریک `T` پاس داده می‌شود، باید از نوع `object` بوده و حتما یک **`property`** با کلید `name` و تایپ `string` داشته باشد.
```ts
class SearchableStore <T> extends Store<T>{
    find(name: string): T | undefined {
      return this._objects.find( (obj) => obj.name === name); // ❌❌
      // Property 'name' dose not exist on type 'T'.
    }
}
```

## استفاده از ورودی ثابت برای جنریک تایپ
```ts
interface Product {
    //...
  }
  class ProductStore extends Store<Product> {
    filterByCategory(category: string): Product[] {
      // filtering process...
      return [];
    }
  }
```

------------------

# محدود کردن جنریک
```ts
function handleInformations <T1, T2 extends T1> (suorce: T1): T2 {
  return Object.apply({}, suorce);
}
```

با این کار میگیم که تایپ T2 حتما باید همه پراپرتی‌های تایپ T1 رو داشته باشه
