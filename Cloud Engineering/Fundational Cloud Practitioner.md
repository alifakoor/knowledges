[[What is Cloud Computing]]
cloud computing is a ecosystem

یک مجموعه فناوری‌ها به سیر تکامل تکنولوژی کمک کردند:
- [[mainframe]] -> [[terminals]]:
	multitasking, many person can use mainframe at same time
	 you don't need to be close to mainframe

- global networks, [[TCP/IP]] (Transmission Control Protocol, Internet Protocol)
	ARPANET -> TCP/IP -> INTERNET
	
**نتیجه:** برداشتن محدودیت فاصله بین کاربران و منابع اتصال به شبکه، مستقل از نرم‌افزار و سخت‌افزار، فقط نیاز بود که هر نود محاسباتی دارای پروتکل TCP/IP باشد

- OS ([[operating system]]), Hardware, [[kernel]], [[Shell]], User Interface -> [[UNIX]], multi user -> 2nd generation of OS

- [[Network Operating System]], NOS, linux, microsoft -> 3th generation of OS
این سیستم عامل‌ها هم multi user هستند اما محدودیتی با این عنوان که کاربر حتما باید بلد باشد با UI یا shell سیستم سرور آشنایی کامل باشه را ندارد
این سیستم عامل‌ها میگن که سرور را در یک جایی قرار می‌دهیم، سرویس سروری را بر روی آن قرار می‌دهیم، کاربر پشت دستگاه خود (کامپیوتر، موبایل و ...) تحت پروتکل TCP/IP ارتباط خودش را با آن سرویس برقرار می‌کند

روش کلاینت-سرور یک رشد بزرگی بود اما هنوز هم یکسری مشکلات دارد، بطور مثال توسعه دهنده باید برای هر نوع device یا ساختاری برنامه خود را توسعه دهد
این مشکل رو با سرویسی به نام WEB حل کرده‌اند، این راه حل اولین بار در آژانس CERN پیاده سازی شد
فایل‌های  html به صورت کدبایت اجرا می‌شوند

برنامه‌هایی که به صورت [[کدبیت]] اجرا می‌شوند وابسته به معماری سخت‌افزار و نرم‌افزار هستند
اما برنامه‌هایی که به صورت [[کدبایت]] اجرا می‌شوند برای اجرا نیاز به یک ابزار دارند مثل browser
تمام browserها وقتی فایلی را میخواهند تفسیر کنند به صورت کدبایت تفسیر می‌کنند، و این یعنی رفتن به سمت استانداردها، دیگر وابسته به معماری سخت‌افزار و نرم‌افزار نیست

بعدها پروتکل‌های http, https بوجود آمدند که صفحات html را در بستر اینترنت در هر جای دنیا به دست کاربر 
می‌رسانند
شرایطی ایجاد شد که UI اپلیکیشن ها توانستند تحت وب برای کاربر نمایش داده شوند


تحت وب کار کردن یعنی اینکه کاربر بتواند به وسیله هر deviceی و با داشتن فقط یک browser به اپلیکیشن مدنظر تحت پروتکل مشخص و شبکه مشخص دسترسی داشته باشد

اما گاهی نیاز هست که این اپلیکیشن‌ها با یکدیگر ارتباط برقرار کنند مانند آن چیزی که در IoT داریم
یکی از تکنولوژی‌هایی که به این قضیه کمک کرد وب‌سرویس یا API بود
وب‌سرویس مجموعه امکاناتی به ما می‌دهد که توسط آن بتوانیم بین اپلیکیشن ها و برنامه‌ها ارتباط برقرار کنیم
که بنیان آن می‌تواند براساس پروتکل http باشد

به طور کلی معماری کلاینت-سرور سبب شد که بتوانیم خدمات را به طور متمرکز بر روی سرورها قرار بدهیم
از طرفی پروتکل‌هایی مثل TCP/IP این امکان را فراهم کردند که بتوان از راه دور با برنامه‌ها کار کرد
این سبب شد که در مجموعه‌ها و سازمان‌ها کامپیوترها به دو دسته خدمات‌دهنده و خدمات گیرنده ([[workstation]]) تقسیم شوند

اهمیت سرور از workstationها خیلی بالاتر است، از نظر معماری سخت‌افزاری و نرم‌افزاری متفاوت هستند
ساعت‌ها و روزها باید بتوانند روشن باشند و کار کنند، منابع مناسبی باید داشته باشد، یک [[orchestrator]] برای مدیریت منابع باید داشته باشد
اهمیت این سرورها اینقدر بالا هستش که جای هیچ خطای سهوی پذیرفته نیست
سازمان‌هایی که به سمت این گونه معماری می‌روند فضای مخصوصی برای نگه داری این سرورها در نظر میگیرند، server room
این فضا نیاز به در نظر گرفتن تمهیدادتی دارد که برای یک سازمان می‌تواند لود هزینه داشته باشد
از طرفی این تکنولوژی ها روز به روز اپدیت می‌شوند و قدیمی ‌می‌شوند
علاوه بر این کلی چالش‌های دیگر دارد

برای این چالش یک راهکاری برون سپاری خدمات به دیتاسنترها با استفاده از انواع [[service provider]]ها از جمله cloud
برون سپاری یا out source کردن یعنی اینکه سازمان‌ها می‌توانند بخشی از لایه‌های مختلف یک برنامه یا اپلیکیشن‌ را به شرکت یا سازمان دیگری بسپارند، در اینجا اصطلاحاتی مثل service provider, cloud بوجود می‌آیند
زمانی که یک سازمان اون لایه های پایین استک رو به کاربرانش خدمات بده، مکانی که این خدمات را میزبانی می کند به آن می‌گوییم دیتاسنتر
در عمل دیتاسنتر مجموعه‌ای هستش که شرایط فیزیکی را فراهم می‌کند که این توانایی را دارند که میزبانی infrastructure را انجام دهند
در مبحث برون‌سپاری پس سازمان‌ها می‌توانند بعضی نگرانی‌ها خود راجع به لایه‌‌های پایین استک را به شرکت‌ها و سازمان‌هایی که این خدمات را ارائه می‌دهند بسپارند
دیتاسنترها اساسا خدماتی مربوط به لایه‌های پایین استک را ارائه می‌دهند

QOS ([[Quality of Service]]): مجموعه تمهیداتی که شما در یک شبکه در نظر می‌گیرید که ترافیک‌های مهم سهم بیشتر یا کیفیت بهتری از خدمات را دریافت کنند

[[offsite]]: انتقال سرور به یک دیتاسنتر

**سرویس پروایدرها:**
مجموعه‌هایی هستند که دیتاسنتر دارند، یا مال خودشون هستش یا اجاره کردند
اما سعی می‌کنند از لایه‌های استک مقادیر بیشتر را برعهده بگیرند و در قالب یک مدل اشتراک منابع (shared responsibility model) میان و بخش بیشتر از لایه‌های استک را برعهده خودشون میگیرند
مثال application service provider
مثلا خیلی از نرم افزارها، sdkها، کامپایلرها و ... رو اون برعهده میگیره
مثال network service provider
که خدمات شبکه‌ای ارائه میده
internet service provider
data center service provider
storage service provider

وب‌سرور یک سرویسی که در edge network قرار داره، چون از یک طرف با کاربران ارتباط داره و از یک طرف با دیتابیس‌ها و اپلیکیشن‌ها و ... در ارتباطه

در عمل در خود دیتاسنترها هنوز هم چالش داریم، مثلا هزینه ریسورس‌های زیاد برای چند روزی در سال که لود بالایی داریم

in cloud -> infrastructure -> storage, network and servers

فناوری‌های virtualization: فناوری‌هایی هستند که روی زیرساخت abstraction ایجاد میکنند، زیرساخت را انتزاعی می‌کنند و در سطحی از انتزاع ریسورس‌ها رو در اختیار کاربران قرار می‌دهند
اینکه سخت‌افزار، ریسورس‌ها و منابع زیرساخت را از چشم کاربر پنهان کنم، یک لایه‌ نرم‌افزاری روی آنها قرار بدهم، و آنها را consolidated، یکپارچه، در قالب resource poolهایی در اختیار کاربر قرار دهم
مثلا ماشین میخوای؟ این در اختیار شما، چیکار داری که ram رو از کجا آوردم
در مجازی سازی underlay را پنهان می کنیم، و یک فضای overlay برای کابران ایجاد می‌کنیم و آنها رو از گرفتاری در مورد مسائل زیرساخت معاف می‌کنیم

[[virtualization]]:
- device or OS level virtualization
- network virtualization
- cluster virtualization
- ...


### Device or OS level virtualization

bare metal virtualization (server virtualization): 
فناوری مجازی‌سازی است که در آن روی یک کامپیوتر (سخت‌افزار) یک نرم‌افزار به نام hypervisor قرار می‌گیرد که این نرم‌افزار شرایطی را ایجاد می‌کند که کاربر بتواند یک ماشین سخت‌افزاری روی آن داشته باشد
روی underlay و سخت‌افزار یک نرم‌افزار قرار میگرد، یک overlay، و روی آن یک ماشین مجازی برای کاربر ایجاد میکنیم

OS level virtualization: 
قبلا در عمل در underlay بیشتر ریسورس‌ها و سخت‌افزار ما قرار میگرفت، اما الان OS هم قرار میگیرد
در روش قبل ما با استفاده از hypervisor به کاربر سخت‌افزار می‌دادیم تا بر روی آنها OS نصب کند
اما آیا می‌توانیم OS را هم در underlay گذاشت و دیگر به کاربر ندهیم؟
مگر کاربر فقط یک اپلیکیشن نمیخواهد؟ آیا نمیتوان فقط آن را با وابستگی‌ها و ملزوماتش به صورت ایزوله اجرا کرد؟
به این بستر ایزوله که شامل خود اپلیکیشن و وابستگی‌های آن است می‌گوییم -> container
و ابزاری که فضا را برای آن ایجاد می‌کند می‌گوییم -> run time engine مثل docker

پس برای میزبانی یک اپلیکیشن در دنیای virtualization دو روش داریم:
اول - استفاده از یک vm که از hypervisor استفاده می‌کند -> device level virtualization
دوم - استفاده از container و run time engine برای این کار -> OS level virtualization -> اپلیکیشن با تمام ملزوماتش


### Network virtualization

VPN ([[Virtual Private Network]]): وقتی که در یک شبکه عمومی چند نود یک شبکه خصوصی تشکیل دهند، بطور مثال با یک زبان دیگر صحبت کنند

مثل قبل باز هم اصلاح underlay رو داریم اینجا، با این تفاوت که در اینجا undelay ما شبکه اینترنت است
در vpn ما می‌توانیم point to point, point to multipoint, multipoint to multipoint داشته باشیم

**دلایل استفاده از vpn:**
محرمانگی - confidentiality - چند نود بتوانند بدون اینکه اطلاعات‌ آنها شنود شود تبادل اطلاعات داشته باشند
یکپارچگی - integrity - سلامت و صحت اطلاعات تبادل شده حفظ شود
کنترل هویت - authentication
داشتن anti-reply
پیاده‌سازی network overlay - داشتن vpn برای اتصال به شبکه خصوصی یک سازمان، انگار مثل قبل روی یک underlay که بستر اینترنت هستش، یک overlay ایجاد می‌کنیم که همون vpn باشه، و بعد با سازمان مربوطه ارتباط برقرار میکنیم

خیلی وقت‌ها vpn رو به عنوان tunneling هم میشناسیم، چند مثال از پروتکل‌ها:
- multiprotocol label switching -> mpls
- Virtual eXtensible Local-Area Network -> vxlan
- Generic Routing Encapsulation Tunnel -> GRE Tunnel

در حوزه امنیت، برای انواع کاربردها مثل احراز هویت و ...:
- IPSec
- Secure socket layer -> SSL

حالا اینها رو چطوری میشه پیاده کرد:
- کپسول کردن - encapsulation
- رمزنگاری - cryptography مثال روش ElGamal، روش Rivest-Shamir-Adleman (RSA)، روشData Encryption Standard (DES)، روش AES
- کنترل صحت اطلاعات - integrity - روشهای md5، sha
- احراز هویت


استانداردسازی در کلاد خیلی مهم است
در حوزه زیرساخت و شبکه اینکه بتوانیم خدمات را استانداردسازی خوب است زیرا که تولیدکنندگان متفاوت این خدمات را تولید می‌کنند و ارائه می‌دهند و ممکن است که باهم سازگار نباشند

[[Software Defined Everything]] - SDE/SDx
امکان تعریف همه چیز به شکل نرم‌افزار را می‌گوییم SDE
Software Defined Network - SDN
Software Defined Storage - SDS

یک تعریف کوتاه از SDN: یک فضای دیتاسنتری در نظر بگیرید، در آنجا چندین سوئیچ وجود داره که هم کار انتقال دیتا بین سرورهای مختلف را به عهده دارند، هم وظیفه اینکه با این دیتاها چیکار بکنند؟
در ساختار سنتی وظیفه اینکه با دیتاها چیکار کنیم به عهده کنترلری هستش که روی خود سوئیچ هست، اما این کار مشکلاتی دارد، لذا باید یک کنترلر مرکزی باشد که این وظیفه را داشته باشد
بطور خلاصه یعنی اینکه بتونم به صورت نرم‌افزاری جریان انتقال اطلاعات و ... رو تعریف کنم

**مزایای استانداردسازی:**
- interoperability
- به راحتی راهکارهای گوناگون میتونن به تبادل اطلاعات بپردازند
- abstraction
- اتوماتیک سازی کارها


![[Pasted image 20240313083559.png]]



در ادامه به بحث [[cloud security]] می‌پردازیم

