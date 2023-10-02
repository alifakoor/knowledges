از زمان پیدایش _ES6_ در سال ۲۰۱۵ ویژگی‌های جدیدی به زبان جاوااسکریپت اضافه شد. یکی از این ویژگی‌ها _ECMAScript Modules_ یا به اختصار _ESM_ است، که فرمت استاندارد رسمی برای بسته‌بندی کدهای جاوااسکریپت برای استفاده مجدد می‌باشد. در یک ماژول، کلاس‌ها، توابع، متغیرها و اشیاء نیز می‌توانند وجود داشته باشند. برای در دسترس قرار دادن همه این‌ها در یک فایل دیگر، می‌توانیم از `export` و `import` استفاده کنیم.

## Export

#### Named Export:
```ts
export let variable_name=1; //متغیر

export function function_name(){} //تابع

export class Class_Name{} //کلاس

// OR

export { variable_name, function_name, Class_Name }
```

#### Default Export:
```ts
const message = () => {
  const name = "Jesse";
  const age = 40;
  return name + ' is ' + age + 'years old.';
};

export default message;
```
از این روش تنها یک بار می‌توانیم در فایل‌ها استفاده کنیم.

--------------

## Import

#### Named Import:
```ts
import { variable_name, function_name } from "./namedExport";

console.log(variable_name)
```

#### Default Import:
```ts
import message from "./defaultExport";

console.log(message)
```



