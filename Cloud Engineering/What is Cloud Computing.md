
cloud computing:
یک اکوسیستم است شامل عوامل انسانی مثل کاربران، ادمین‌ها، متخصصین
مجموعه‌ای از فناوری‌ها در زیرساخت مربوط به storage, virtualization, network, server
گروهی از orchestratorها، ابزارهای مانیتورنیگ، پورتال‌ها
این مجموعه با هم دیگر تکنولوژی‌هایی ایجاد میکنند که خدماتی را از آن resourceها به کاربران ارائه دهند، که در راستای اهداف سیر تکنولوژی هستند مثل high availability, automated, ...

NIST: National Institute of Standards and Technology

تعریف cloud در NIST: ارائه خدمات آنلاین به شکلی که automated باشد، scalable باشد و کاربر بتواند pay as you go پرداخت داشته باشد

![[Pasted image 20240314090406.png]]

در تعریف NIST آماده است که cloud یکسری Essential Characteristics دارد، یکسری خدمات در قالب [[Service Models]] ارائه می‌دهد و انواع توسعه مختلفی دارد، Deployment Models


### Essential Characteristics:
یکی از افتخارات cloud این است که خدمات را می‌تواند scalable ارائه دهد، اگر کاربر خدمتی گرفته است و لود آن بالا یا پایین رفت، on-demand ریسورس را کم یا زیاد می‌کند آن هم به صورت اتوماتیک، و حتی نه وقتی که کاربر گفت، اگر از روی دیتاهای مانیتور شده به این نتیجه برسه که باید ریسورس کم و زیاد شود، این کار به صورت اتوماتیک انجام می‌شود
Broad Network Access: خدمات هر زمان و هر کجا, any where, any time
کلاد میگه برای خدماتت هر کجا خواستی بشین، به شبکه TCP/IP متصل شو، من اگر بخوای یک network overlay هم برات میزنم
از طرف دیگر سیستم کلاد اجایل کار می‌کند، منظور همون چابکی سیستم است
اساسا کلاد پرووایدرها بر رویه distributed processing کار می‌کنند
یکی از شعارهای کلاد این هستش که من خدمات را از نزدیکترین نقطه به کاربران میدهم، [[CDN]]، edge computing
موضوع pay as you go که کاربر هر چقدر از خدمات استفاده کند، هزینه پرداخت می‌کند

کلاد دوای همه دردها نیست، چالش‌هایی نیز ایجاد می‌کند، مثلا امنیت
امنیت هم می‌تونه یه مزیت برای کلاد باشه، هم میتونه یه چالش باشه
خیلی هم واضح هستش، وقتی منابع رو به یک کلاد پرووایدر برون سپاری کردین،‌ داده شما پیش خودتون نیست
وقتی داده شما پیش کس دیگه‌ای هستش، آیا اون مثل شما حساسه؟ آیا درکی از security policy دارد؟
یا این رو در نظر بگیرید که اون کلاد پرووایدر تحت قوانین کشوری که در آن کار می‌کند باید اطلاعات را به مراجع ذی‌ربط بدهد
مساله کنترل، وقتی شما سرویس یا داده خودتون را دادین به یه کلاد پرووایدر، دیگه تحت کنترل شما نیست
شما دقیقا باید بدونین که کلاد چیکار میکنه تا اگر اتفاقی افتاد مثل disaster بدونیم که مقصر کی هستش

بهترین مکان برای میزبانی خدمات کلاد همان دیتاسنترها هستند با ویژگی‌هایی که قبلا گفتیم

[[fog computing]]: کلاد را بخاطر چالش‌هاش نزاریم کنار، چون فواید زیادی دارد، بیایم یکسری از تصمیم‌گیرنده‌ها رو نزدیک منبعی که داده‌ها تولید میشن قرار بدین،‌ near by source، و یکسری تصمیم‌های حیاتی و فورس در آنجا گرفته شود و این فاگ نودها با کلاد در ارتباط باشند


معماری یک کلاید پرووایدر به چه صورت است؟ [[Cloud Architecture]]


برای مهاجرت از یک زیرساخت سنتی به زیرساخت کلد باید چه مواردی را در نظر گرفت؟ [[cloud development model]]


[[اصطلاحات cloud]]
