ممکن است برخی آبجکت‌ها پراپرتی‌های زیادی داشته باشند و مشخص کردن نام تمام آن‌ها موقع تعریف کردن آبجکت، کد را شلوغ کند. اگر بخواهیم بدون داشتن لیست مشخصی از نام پراپرتی‌ها آبجکت بسازیم از این روش استفاده می‌کنیم:
```ts
const foodObject: { [index: string]: string } = {};
foodObject.name= "kabab"
foodObject.chef = "reza";
foodObject.recipes = "meat, rice, onion";
```

