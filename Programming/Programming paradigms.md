![[paradigms.png]]

## برنامه‌نویسی دستوری (Imperative programming)

در برنامه‌نویسی `imperative` تمرکز بر توصیف نحوه‌ی انجام کار است و دستوراتی که قدم به قدم بر روی یک یا چند متغیر اجرا می‌شوند.
```ts
for (let i: number = 0; i < 10; i++) {
  console.log(i);
}
```
programming languages: Java, C, Pascal, Python, Ruby, Fortran, PHP

### برنامه‌نویسی پروسه‌ای (Procedural programming)
برای کنترل بیشتر برنامه، گام‌های برنامه را به پروسه‌های جدا تقسیم می‌کنیم. پروسه به معنی توابعی است که هر کدام شامل مراحل و وظایفی برای اجرا هستند.

### پردازش موازی (Parallel processing)
در `Parallel processing` برنامه به بخش‌های کوچک‌تری تقسیم می‌شود و این بخش‌ها به صورت هم‌زمان اجرا می‌شوند تا زمان کم‌تری برای حل مسئله صرف شود.

### برنامه‌نویسی شیءگرا (Object oriented programming)
در این روش محور اصلی برنامه شیءها هستند، شیءها از داده‌ها و متدها تشکیل شده‌اند.
کپسوله‌سازی (`Encapsulation`)، ارث‌بری (`Inheritance`)، چندریختی (`Polymorphism`)، انتزاع (`Abstraction`)



## برنامه‌نویسی اعلانی (Declarative programming)
برنامه‌نویسی `declarative` بر چیستی تمرکز دارد، یعنی بر نتیجه‌ی کار تاکید دارد. در واقع در نوشتن کد `declarative` ابتدا این سوال مطرح است که از برنامه‌ی خود چه می خواهید.
```ts
const add = (x: number, y: number): number => x + y;
let result = add(2, 3);
console.log(result); // 5
```
programming languages: SQL, Miranda, Prolog, Lisp, ...

### برنامه‌نویسی منطقی (Logical programming)
برنامه‌نویسی `logical` بر پایه منطق است. در واقع یک سری حقایق و قوانین داریم و با توجه به این حقایق، به اظهارات جدیدی می‌رسیم.

### برنامه‌نویسی تابعی (Functional programming)
برنامه ترکیبی از چندین تابع و فراخوانی آن‌هاست. در برنامه‌نویسی `functional` اصولی همچون، توابع خالص (`Pure Functions`)، تغییرناپذیری (`Immutability`)، توابع مرتبه بالا (`Higher-Order Functions`) و ... مطرح می‌شوند