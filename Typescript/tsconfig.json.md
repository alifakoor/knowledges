```json
{
  "compilerOptions": {
    /* Visit https://aka.ms/tsconfig to read more about this file */
    /* Projects */
    // "incremental": true,                              /* فایلی ایجاد و اطلاعات آخرین کامپایل را در آن ذخیره می‌کند تا امکان کامپایل تدریجی پروژه فراهم شود. */
    // "composite": true,                                /* محدودیت های خاصی را فعال می‌کند و به  پروژه تایپ‌اسکریپت اجازه می‌دهد تا با ارجاعات پروژه استفاده شود. */
    // "tsBuildInfoFile": "./.tsbuildinfo",              /* مسیر فایل کامپایل تدریجی را مشخص می‌کند.(.tsbuildinfo) */
    // "disableSourceOfProjectReferenceRedirect": true,  /* در زمان کار با پروژه های تایپ‌اسکریپت ترکیبی، راهی برای بازگشت به رفتار نسخه قبل از 3.7 فراهم می کند که در آن فایل های d.ts به عنوان مرز بین ماژول ها استفاده می شد. */
    // "disableSolutionSearching": true,                 /* هنگام ویرایش، یک پروژه را از بررسی مرجع چند پروژه خارج می کند. */
    // "disableReferencedProjectLoad": true,             /* تعداد پروژه هایی که به طور خودکار توسط تایپ‌اسکریپت لود می‌شوند را کاهش می‌دهد. */
    /* Language and Environment */
    "target": "es2016",                                  /* نسخه‌ی جاوا اسکریپتی که کد تایپ‌اسکریپت به آن تبدیل می‌شود را مشخص می‌کند. */
    // "lib": [],                                        /* مشخص می‌کند چه ویژگی ها و اشیاء پیش فرضی را پشتیبانی کند. */
    // "jsx": "preserve",                                /* مربوط به کار با کتابخانه react است و مشخص می کند چه کد JSX تولید می شود. */
    // "experimentalDecorators": true,                   /* پشتیبانی آزمایشی برای دکوراتورها را فعال می‌کند. */
    // "emitDecoratorMetadata": true,                    /* پشتیبانی آزمایشی برای انتشار نوع متادیتا برای دکوراتو‌رها را فعال می‌کند. */
    // "jsxFactory": "",                                 /* تابعی که در فایل‌های .js فراخوانی می‌شوند، در زمان کامپایل المان‌های JSX از runtime  کلاسیک JSX استفاده می‌کند. */
    // "jsxFragmentFactory": "",                         /* مرجع JSX Fragment مورد استفاده را مشخص می‌کند */
    // "jsxImportSource": "",                            /* مشخص می‌کند ماژول مورد استفاده برای ایمپورت JSX factory functions هنگام استفاده از 'jsx: react-jsx*' چیست. */
    // "reactNamespace": "",                             /* شیء فراخوانی شده برای 'createElement' را مشخص می‌کند. تنها زمانی که react برای JSX اعمال شده. */
    // "noLib": true,                                    /* اگر این گزینه فعال شود، lib نادیده گرفته می‌شود. گنجاندن خودکار فایل‌های کتابخانه‌ای را غیرفعال می کند. */
    // "useDefineForClassFields": true,                  /* این گزینه رفتار کامپایلر را به نسخه استاندارد ECMAScript فیلدهای کلاس تغییر می‌دهد. */
    // "moduleDetection": "auto",                        /* روش شناسایی فایل‌های جاوااسکریپت ماژولار را مشخص می‌کند.*/
    /* Modules */
    "module": "commonjs",                                /* مشخص می‌کند چه کد ماژولی تولید می‌شود. */
    // "rootDir": "./",                                  /* پوشه root را در فایل‌های منبع مشخص می‌کند. */
    // "moduleResolution": "node",                       /* مشخص می‌کند تایپ‌اسکریپت چگونه یک فایل را در module specifier مشخص شده جستجو کند. */
    // "baseUrl": "./",                                  /* دایرکتوری پایه‌ای را به حل نام ماژول های غیر نسبی اختصاص می‌دهد. */
    // "paths": {},                                      /* مجموعه‌ای از ورودی‌ها را دریافت می کند که import ها را برای جستجوی مکان‌های مربوط به baseUrl می‌سنجد. */
    // "rootDirs": [],                                   /* با استفاده از rootDirs، می توانید به کامپایلر اطلاع دهید که تعداد زیادی دایرکتوری مجازی وجود دارد که به عنوان یک ریشه واحد عمل می کنند. */
    // "typeRoots": [],                                  /* می‌توانید چندین پوشه را مشخص کنید که مانند "./node_modules/@types" عمل کنند. */
    // "types": [],                                      /* می‌توانید تایپ نام پکیج‌ها را مشخص کنید تا بدون ارجاع در فایل منبع گنجانده شوند. */
    // "allowUmdGlobalAccess": true,                     /* جازه دسترسی به UMD از ماژول ها را به صورت سراسری می‌دهد. */
    // "moduleSuffixes": [],                             /* لیست پسوند نام فایل‌ها را برای جستجو در هنگام حل یک ماژول می‌گیرد. */
    // "resolveJsonModule": true,                        /* امکان import  فایل‌های json. را فعال می‌کند. */
    // "noResolve": true,                                /* اجازه نمی‌دهد ایمپورت‌ها ، requireها یا <reference> ها از تعداد فایل‌هایی که تایپ‌اسکریپت باید به پروژه اضافه کند بیشتر شوند.    */
    /* JavaScript Support */
    // "allowJs": true,                                  /* امکان استفاده فایل‌های جاوااسکریپت را در میان فایل‌های تایپ‌اسکریپت را به ما می‌دهد. */
    // "checkJs": true,                                  /* خطاهای موجود در فایل‌های جاوا اسکریپت را گزارش می‌دهد. */
    // "maxNodeModuleJsDepth": 1,                        /* حداکثر عمق پوشه‌ها برای بررسی فایل‌های جاوااسکریپت از 'node_modules' را مشخص می‌کند. فقط با 'allowJs' قابل اجرا است.*/
    /* Emit */
    // "declaration": true,                              /* مسئول ساخت فایل‌های .d.ts از فایل های تایپ‌اسکریپت و جاوااسکریپت در پروژه است. */
    // "declarationMap": true,                           /* یک sourcemap برای فایل های d.ts ایجاد می‌کند. */
    // "emitDeclarationOnly": true,                      /* فقط فایل‌های d.ts را خروجی بگیرد و نه فایل‌های جاوا اسکریپت. */
    // "sourceMap": true,                                /* فایل های sourcemap را ایجاد می‌کند. */
    // "outFile": "./",                                  /* فایلی را مشخص می‌کند که همه خروجی‌ها را در یک فایل جاوااسکریپت جمع کند. اگر «اعلان» درست باشد، فایلی را  برای خروجی‌های .d.ts مشخص می‌کند */
    // "outDir": "./",                                   /* مسیری که فایل های کامپایل شده را در آن قرار می‌گیرد. */
    // "removeComments": true,                           /* در هنگام کامپایل تمام کامنت ها را حذف می کند. */
    // "noEmit": true,                                   /* هیچ فایل جاوا اسکریپتی ایجاد نخواهد شد. */
    // "importHelpers": true,                            /* اجازه وارد کردن توابع کمکی از tslib را یک بار در هر پروژه می‌دهد، به جای اینکه آن‌ها را در هر فایل اضافه کند. */
    // "importsNotUsedAsValues": "remove",               /* نحوه عملکرد import ها را کنترل می کند. */
    // "downlevelIteration": true,                       /* مطمئن می‌شود که حلقه‌ها و کدها در مواردی که تارگت خیلی قدیمی است، با دقت بیشتری کامپایل شوند. */
    // "sourceRoot": "",                                 /* مسیر اصلی را برای دیباگرها برای یافتن کد منبع مشخص می کند. */
    // "mapRoot": "",                                    /* مکانی را مشخص می‌کند که debugger باید map files ها را به جای مکان ایجاد شده در آن قرار دهد. */
    // "inlineSourceMap": true,                          /* فایل‌های sourcemap در جاوا اسکریپت منتشر شده قرار گیرد. */
    // "inlineSources": true,                            /* کد منبع را در sourcemap هایی که در جاوااسکریپت منتشر شده قرار می‌دهد. */
    // "emitBOM": true,                                  /* یک علامت UTF-8 Byte Order Mark (BOM) در ابتدای فایل های خروجی قرار می‌دهد. */
    // "newLine": "crlf",                                /* کاراکتر خط جدید را برای ارسال فایل‌ها تنظیم می‌کند. */
    // "stripInternal": true,                            /* برای کدهایی که دارای @internal در کامنت‌های JSDoc هستند، اعلان ارسال نکند. */
    // "noEmitHelpers": true,                            /* غیرفعال کردن ایجاد توابع کمکی سفارشی مانند '__extends' در خروجی کامپایل شده. */
    // "noEmitOnError": true,                            /* در صورتی که خطایی در یکی از فایل‌ها وجود داشت، فایل‌ها کامپایل نمی‌شوند. */
    // "preserveConstEnums": true,                       /* پاک کردن اعلان‌های "const enum" در کد ایجاد شده را غیرفعال می‌کند. */
    // "declarationDir": "./",                           /* دایرکتوری خروجی فایل های اعلان ایجاد شده را مشخص می‌کند. */
    // "preserveValueImports": true,                     /* مقادیر import  شده که استفاده نشده‌اند را در خروجی جاوااسکریپت حفظ می‌کند، در صورت فعال نبودن حذف می‌شوند. */
    /* Interop Constraints */
    // "isolatedModules": true,                          /* اطمینان حاصل می‌کند که هر فایل بدون در نظر گرفتن import های دیگر ترنسپایل می‌شود. */
    // "allowSyntheticDefaultImports": true,             /* اجازه می‌دهد زمانی که default export انجام نشده، به صورت 'import x from y' عمل شود.  */
    "esModuleInterop": true,                             /* کامپایلر از کدهای خاصی برای بررسی شیء import شده استفاده می‌کند تا تشخیص دهد که آیا Exports پیش‌فرض است یا شیء Exports که بازنویسی شده. سپس آن را کامپایل می‌کند. */
    // "preserveSymlinks": true,                         /* مسیر واقعی symlink ها را غیرفعال می‌کند. */
    "forceConsistentCasingInFileNames": true,            /* از درست بودن حروف import ها اطمینان حاصل می‌کند. */
    /* Type Checking */
    "strict": true,                                      /* بررسی تایپ ها را سخت گیرانه می‌کند. با فعال کردن این گزینه تمام گزینه های بعد فعال می‌شوند. */
    // "noImplicitAny": true,                            /* اگر تایپ any وجود داشت و کاربر آن را تعریف نکرده بود گزارش خطا می‌دهد. */
    // "strictNullChecks": true,                         /* هنگام بررسی تایپ، "null" و "undefined" را در نظر می‌گیرد. */
    // "strictFunctionTypes": true,                      /*  باعث می‌شود که پارامترهای توابع به درستی بررسی شوند. */
    // "strictBindCallApply": true,                      /* مطمئن می شود که از توابع bind یا call یا apply به صورتی استفاده شده است. */
    // "strictPropertyInitialization": true,             /* پراپرتی‌های کلاس را که اعلان شده‌اند ولی در سازنده تنظیم نشده‌اند را بررسی می‌کند. */
    // "noImplicitThis": true,                           /* هنگامی که "this" تایپ "any" داده می شود، گزارش خطا می‌دهد. */
    // "useUnknownInCatchVariables": true,               /* اجازه می‌دهد که تایپ متغیرها در catch clause از any به unknown تغییر کند.  */
    // "alwaysStrict": true,                             /* اطمینان حاصل می‌کند که از 'use strict' استفاده می شود. */
    // "noUnusedLocals": true,                           /* اگر متغیرهای محلی تعریف شده‌اند باید از آن ها استفاده شود.  */
    // "noUnusedParameters": true,                       /* پارامترهای تعریف شده و بدون استفاده مجاز نیستند. */
    // "exactOptionalPropertyTypes": true,               /* قوانین سخت گیرانه‌ای برای ‌‌پراپرتی‌های اختیاری در نظر می‌گیرد و نمی‌توان به آن‌های مقدار undefined داد. */
    // "noImplicitReturns": true,                        /*  نباید توابعی باشند که گاهی مقداری را return کرده و گاهی مقداری return نکنند. */
    // "noFallthroughCasesInSwitch": true,               /* فعال کردن گزارش خطا برای مواردی که در سوئیچ کیس به مشکل می‌خورد. */
    // "noUncheckedIndexedAccess": true,                 /* هنگامی که با استفاده ازindex به فیلدی که تعریف نشده دسترسی پیدا می‌کند، undefined را اضافه می‌کند. */
    // "noImplicitOverride": true,                       /* کلاسی که در یک کلاس مشتق شده override شود باید کلمه‌ی کلیدی override بگیرد. */
    // "noPropertyAccessFromIndexSignature": true,       /* برای دسترسی به فیلدی که اعلان نشده است، از index (obj["key"]) استفاده کنید. */
    // "allowUnusedLabels": true,                        /* گزارش خطا را برای لیبل‌های استفاده نشده غیرفعال می‌کند. */
    // "allowUnreachableCode": true,                     /* برای کد غیرقابل دسترس گزارش خطا را غیرفعال می‌کند. */
    /* Completeness */
    // "skipDefaultLibCheck": true,                      /* از بررسی تایپ فایل‌های .d.ts که در تایپ‌اسکریپت هستند صرف نظر می‌کند. */
    "skipLibCheck": true                                 /* از بررسی تایپ فایل‌های .d.ts صرف نظر می‌کند. */
  }
}
```
