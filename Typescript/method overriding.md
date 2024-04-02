به مثال زیر دقت کن:
```ts
export class Account {
  id: number;
  owner: string;
  balance: number;

  constructor(id: number, owner: string, balance: number) {
    this.id = id;
    this.owner = owner;
    this.balance = balance;
  }

  withdraw(amount: number) {
    this.balance -= amount + amount * 0.02;
  }
}
```

حالا اگر یه کلاس دیگه بخوایم که ازین کلاس ارث بری کنه و متد `withdraw` رو بخوایم دوباره بنویسیم یا منطقشو عوض کنیم چی؟
```ts
import { Account } from './account';

class VipAccount extends Account { 

  override withdraw(amount: number) { 
    this.balance -= amount + amount * 0.01;
  }
 }
```

اگر کلیدواژه‌ی `override` را پیش از نام متد ننویسیم متوجه می‌شویم که کد ما همچنان به درستی کار می‌کند و وجود این کلید‌واژه ضروری نیست.

پس دلیل نوشتن `override` چیست؟

> درواقع با استفاده از این کلید‌واژه به تایپ‌اسکریپت می‌گوییم که این متد بازنویسی شده‌ی متد قبلی است و صرفا بدنه‌ی آن بازنویسی شده. همچنین در صورتی که در نوشتن نام متدی که قصد بازنویسی آن را داریم غلط املایی داشته باشیم خطا دریافت می‌کنیم و از باگ‌های احتمالی پیشگیری ‌می‌کنیم.

پیشنهاد می‌شود در فایل `tsconfig.json` کامپایلر آپشن `noImplicitOverride` را فعال کنید تا درصورتی که فراموش کردید از این کلید‌واژه استفاده کنید، خطای مناسب دریافت کنید.

**`tsconfig.json`**
```json
{
  "compilerOptions": {
    "noImplicitOverride": true,
  },
  "include": [
    "src"
  ]
}
```


### گسترش متدها
```ts
import { Account } from './account';

class BadAccount extends Account {
  debt: number;

  constructor(id: number, owner: string, balance: number,
   debt: number) {
    super(id, owner, balance);
    this.debt = debt;
  }

  override withdraw(amount: number) {
    super.withdraw(amount);
    this.balance -= amount * 0.01; // extra 1% fee for badAccounts
  }
}

function printOwner(accountList: Account[]) {
  for (const account of accountList) {
    console.log(account.owner);
  }
}
```

بتدا عملیات `withdraw` را همانگونه که در کلاس والد انجام میدادیم انجام می دهیم (`super.withdraw(amount)`).

سپس مقدار بیشتری کارمزد از موجودی کاربر کم می‌کنیم (`this.balance -= amount * 0.01`).



-----------------
### نکته
برای نوشتن پراپرتی‌ها میتونیم اینکار رو هم بکنیم
```ts
abstract class Shape {
  constructor(public name: string) {
    this.name = name;
  }
}
```

