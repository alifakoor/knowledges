![[Pasted image 20240330101617.png]]

کلادها از نظر معماری فرقی باهم ندارند
اما public cloud اومده که در دسترس عموم مردم باشه و خدماتش رو به عموم مردم بده

یک public cloud سعی میکنه اون معماری کلاد صاحبش خودش باشه، حالا اینکه دیتاسنتر مال خودش هست یا نه رو کاری نداریم
منظور اینکه اون cloud architecture و software stack رو از جایی اجاره نمیکنه، اون‌ها رو سعی میکنه مال خودش باشه
یه جورایی [[on-premise]] است (در مقابل [[off-premise]])

یک پابلیک کلاد [[multi tenancy]] است در مقابل [[single tenancy]]

یک پابلیک کلاد اتصال به اینترنت دارد، یعنی کاربران یک پابلیک کلاد غالبا از یک بستر عمومی استفاده میکنن و متصل میشن به کلاد و خدماتشون رو میگیرن

زندگی یک کلاد پرووایدر به این بستگی دارد که اینترنت باشد
کلاد پرووایدر یک ISP نیست

چالش‌های پابلیک کلاد چیست؟
![[Pasted image 20240402083339.png]]


### **چالش‌های مربوط به امنیت:**
وقتی شما تصمیم گرفته‌اید که از یک زیرساخت کلاد استفاده کنید یعنی اینکه قرار شده شما برخی از خدماتتون رو روی کلاد بزارید و اون میزبانی بکنه، و شما پذیرفته‌اید که داده‌های شما در جایی بیرون از سازمانتون میزبانی بشن
مثلا دیتاسنتری که کلاد پرووایدر داره ازش استفاده میکنه برحسب اتفاقی از بین رفت چی؟ اصلا مقصر کلاد پرووایدر هم نیست
باید ببینید که [[security policy]] شما چی هست؟ که خط قرمز شما چیه؟ اون چیزی که باید ازش حفاظت کنید چیه؟ اگر نبود چقدر ضربه میخورید؟
![[Pasted image 20240402083920 1.png]]

اینترنت خیلی مهمه در اینجا، شرکت‌های isp خیلی نقش ایفا میکنن، چون بالاخره ارتباط شما با کلاد پرووایدر و مشتری شما با خدماتی که بر روی کلاد میزبانی میشن از طریق اینترنت هست دیگه
مثلا خدمت شما استریمینگ هست، اگر قرار باشه بستر اینترنت کیفیت خوبی نداشته باشه و خدمت شما با اختلال روبرو بشه، در واقع امنیت کسب و کار شما به خطر افتاده دیگه

این رو هم در نظر بگیرید که امنیت رو جدی بگیرید، efficiency پایین میاد، این یک دعوای بی‌پایانه بین شبکه‌ کارها که efficiency رو میخوان با امنیت‌کارها که میگن هر چیزی که راحتتره خطراتی هم داره دیگه

در حوزه امنیت همیشه بیشترین آسیب از سمت نیروهایی زده می‌شوند که یا توجیه نشده‌اند و یا اینکه بطور مثال آدم حفاظت اطلاعات نیستند، لزوما هر شخصی که امنیت میدونه، کسی نیست که بتونه یک راز رو همیشه حفظ کنه


### **چالش‌های مربوط به کنترل:**
این چالش‌ها شبیه به چالش‌های مربوط به امنیت هستند، چون وقتی شما بطور مثال سیستم کولینگ اتاق سرورها رو به درستی کنترل نکنید و دما بالا برود و سرورها از کار بیفتند، با زمانی که یک حمله صورت گرفته و سرورها از کار افتادن فرقی نمی‌کنه

اصلی‌ترین چالش مربوط به کنترل این هستش که وقتی شما از یک کلاد پرووایدر پابلیک استفاده میکنید، این کلاد پرووایدر ممکن است از دیتاسنترهای مختلفی استفاده کنند که ممکن است بعضی از این دیتاسنترها در خارج از کشور باشند و در دیگر کشورها قرار گرفته باشند، و طبق قوانین آن کشور عمل کنند

![[Pasted image 20240404083733.png]]

مساله بعدی اینکه کلاد ارائه خدمات را خیلی ساده می‌کند، این سادگی ممکن است از اون طرف هم ما رو بندازه و هزینه ایجاد کنه برای ما
![[Pasted image 20240404083933.png]]


مساله بعدی در نظر گرفتن ملاحظات فنی و process، این رو در نظر بگیرید که مثلا خدمت شما استریمینگ هستش، برای داشتن یک استریمینگ خوب خیلی وابستگی‌ها هستش، مثلا خود بستر اینترنت، حالا این رو در نظر بگیرید که مشکلی پیش بیاد، isp میگه مشکل از من نیست، cloud میگه مشکل از من نیست، پس باید یک مانیتورینگ عالی داشته باشیم که بتونیم تشخیص بدیم دقیقا مشکل از کجا نشات میگیره

قرارداد SLA ([[service level agreement]]) حتما باید در نظر گرفته بشه

![[Pasted image 20240404084128.png]]


### **چالش‌های مربوط به هزینه:**
مساله بعدی کنترل هزینه‌ها و هزینه‌های پنهان هستش

