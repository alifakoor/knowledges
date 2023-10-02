## تایپ سودمند خودتان را بسازید
```ts
  type CreateMutableAndRequired<Type> = {
    -readonly [Property in keyof Type]-?: Type[Property];
  };

  type LockedAccount = {
    readonly id: string;
    readonly name: string;
  };

  type UnlockedAccount = CreateMutableAndRequired<LockedAccount>;
```

در این قطعه کد `CreateMutableAndRequired` همه‌ی پراپرتی‌های تایپ ورودی را:

1. قابل خواندن (`-readonly`) :
    
    > با قرار دادن علامت `-` قبل از کلید‌واژه‌ی `readonly` ویژگی `readonly` بودن را حذف کرده و **پراپرتی**‌های مورد نظر را قابل تغییر می‌کند.
    
2. اختیاری می‌کند ( `Property in keyof Type]-?`) :
    
    > با قرار دادن علامت `-` قبل از `? (question mark)` ویژگی اختیاری بودن پراپرتی‌های مورد نظر را حذف می‌کند و به بیانی دیگر اجباری می‌کند.
    

https://javascript.plainenglish.io/using-typescript-mapped-types-like-a-pro-be10aef5511a