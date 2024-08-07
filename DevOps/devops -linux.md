***نکته: ویدئو مربوط به نصب لینوکس را داکیومنت نکردی***

دوتا از ابزارهایی که برای اتوماتیک‌سازی نصب و راه‌اندازی محیط استفاده می‌شوند، [[packer]] و [[vagrant]] هستند

در ابزار [[vagrant]] ما می‌تونیم از روی یک ایمیج فایلی یه محیط و یا به اصطلاح environment بیاریم بالا و به راحتی ست کنیم که مشخصاتش چی باشه

ابزار [[packer]] این امکان رو به ما میده که ما به وسیله اون بتونیم یک ایمیج آماده کنیم

این نکته را در نظر بگیرید که در اینجا ایمیجی که ازش صحبت می کنیم، ایمیج‌های virtual machineهاست، هرچند که ابزار [[packer]] ایمیج داکر هم می‌تواند ایجاد کند.

***در توزیع‌های مختلف پیشنهاد می‌شود که برای یادگیری یکبار توزیع arch linux را از روی how to... خودش نصب کنید***

سایت [distrowatch.com](https://distrowatch.com) اپدیت توزیع‌های مختلف را میزاره


## معماری لینوکس
![[Pasted image 20240509085755.png]]

#### process management

![[Pasted image 20240509090002.png]]

پراسس را یک instance از اون برنامه، اپلیکیشن یا نرم‌افزار ما هست که این پراسس typeهای مختلف داره، میتونه single thread یا multi thread باشه

پراسس‌ها می‌تونن foreground یا background باشند

daemon: سرویسی است که در بکگراند ران شده است و ما می‌تونیم مدیریتش کنیم

حالا ما برای اینکه بتونیم پراسس‌هامون رو ببینیم نیاز به یه utility داریم
این utility حتما نباید یک gui باشه، میتونه یک command باشه

هر پراسس چند state دارد:
create
ready
waiting
running
terminating
stop

یعنی یک پراسس در طول زمان حیات خودش در هر لحظه در یکی از این stateها قرار میگیرد، state مطلوب ما برای یک پراسس running است که در آن پراسس اجرا شده و داره کار خودشو میکنه

یکسری پراسس‌ها وجود دارند که به آنها پراسس‌های zombie میگیم، پراسس‌هایی که parent ندارند

![[Pasted image 20240509091331.png]]


اپلیکیشن‌ها و پراسس‌ها می‌تونن single thread یا multi thread باشند
هر core فیزیکی cpu به ما دو تا thread میده


### کامندهای پرکاربرد
**bg, fg, jobs:**

![[Pasted image 20240509091646.png]]

![[Pasted image 20240509091907.png]]

**jobs:** show all background process

**kill -9:** در جا پراسس را میکشد و صبر نمیکنه که پراسس کارش تموم بشه

![[Pasted image 20240509101007.png]]


در کامند htop قسمت load average اگر برابر با تعداد cpu's core بود یعنی اینکه از ۱۰۰درصد cpu داره استفاده میشه

به وسیله xargs می‌تونیم خروجی یه دستور رو بگیریم بدیم به ورودی دستور بعدی، مثلا
```sh
pidof nginx | xargs sudo kill -9
```



### package manager

پکیج چیست؟
پکیج یه اپلیکیشن با همه دور و بری‌هاشه، یعنی هرچیزی که اون اپلیکیشن نیاز داره، مثل dependencyهایی که لازم داره یا دیتایی که لازم داره

پکیج منیجر این امکان رو به ما میده تا این پکیج‌ها رو به راحتی نصب کنیم

به طور خلاصه، یکسری ریپازیتوری وجود دارد، مثل یکسری مکان در نظر بگیرید، پکیج‌ها در این ریپازیتوری‌ها ذخیره میشن، لیست این پکیج‌ها در یکسری دیتابیس در سیستم ما قرار داره، و ما با اجرای دستوری مثل `apt update` در واقع اون لیست را به روز می‌کنیم، و وقتی دستور نصب را اجرا می‌کنیم میره اون لیست رو میخونه و اگر پیدا کرد از ریپازیتوری مشخصی که برای اون پکیج هست اون رو دریافت میکنه و نصب میکنه

ما در اوبونتو از پکیج منیجر apt (advance package tool) استفاده می‌کنیم
بعضی از دستورات این پکیج منیجر:
```sh
apt update
apt upgrade
apt install
```

داخل دایرکتوری `/etc/apt` تمام کانفیگ این پکیج منیجر اونجاست و ما می‌تونیم اونها رو تغییر بدیم

***نکته: در لینوکس همه چیز فایل است و شما می‌توانید با تغییر فایل‌ها تمام کانفیگ‌ها رو عوض کنید.

برای اینکه این پکیج منیجر مطمئن باشه که از ریپازیتوری‌های قابل اطمینانی داره پکیج رو دریافت می‌کنه، قبل از دریافت پکیج از یک [[GPG key]] استفاده میکنه به این صورت که اول این [[GPG key]] رو دریافت می‌کنه و بعد در درخواست بعدی برای دریافت پکیج از اون استفاده میکنه تا مطمئن باشه که داره پکیج رو از ریپازیتوری رسمی دریافت می‌کنه

با دستوری `apt-key list` میتونیم لیست این کلیدها رو ببینیم
همچنین در مسیر `/etc/apt/trusted.gpg.d` این لیست موجود است

با کامند `dpkg -i`  هم می‌توان یک پکیج را از طریق فایل `.deb` آن نصب کرد


لیست repositoryهای موجود در ubuntu رو میشه در فایل `/etc/apt/source.list` پیدا کرد، یک دایرکتوری `source.list.d` نیز در این مسیر وجود دارد که معمولا این `.d`ها اضافه بر سازمان هستند،‌ مثلا شما در فایل `source.list` لیست repositoryها رو دارین و در دایرکتوری `source.list.d` اون repositoryهای اضافه رو دارین

***نکته:***
وقتی شما دستور `apt update` رو اجرا می‌کنید، سیستم میره این لیست repositoryها رو میخونه و از روی این لیست شروع میکنه یه دیتابیسی رو داخل خودش اپدیت میکنه که در اون دیتابیسه داره لیست پکیج‌ها رو قرار میده
و بعد وقتی دستور `apt install nginx` رو اجرا می‌کنیم، از روی این لیست repositoryها، میدونه nginx در کدام repository هستش و میره اون رو از اون repository میگیره و نصب می‌کنه

با اجرای دستور `apt upgrade` پکیج‌هایی که در این repositoryها وجود دارند اپدیت می‌شن

با اجرای دستور `apt autoremove` سیستم خودکار وابستگی‌های پکیج‌های مختلف که deprecate شدن رو پاک میکنه

دستور `apt remove [package_name]` پکیج رو پاک میکنه
دستور `apt purge [package_name]` هم پکیج رو پاک میکنه هم فایل‌های اون پکیج رو حذف میکنه


#### proxy for apt:
برای ست کردن پروکسی برای پکیج منیجر apt کافی است که در مسیر `/etc/apt/apt.conf.d` یک فایل به طور مثال با نام `01proxy` بسازید با محتوای زیر:
```sh
Acquire::http::Proxy "http://127.0.0.1:8123";
Acquire::https::Proxy "http://127.0.0.1:8123";
```

 خوبه که پروکسی ست کنیم برای این پکیج منیجر و خوبه که ignore proxy هم داشته باشیم، تا مثلا برای پکیج‌‌هایی که از داخل ایران قراره بگیره دیگه نره خارج ایران و برگرده



### systemd

این سرویس در لینوکس به عنوان سرویس اول میاد بالا و pid = 1 را می‌گیرد و کارش هم مدیریت بقیه سرویس‌ها هستش و اصطلاحا اونها رو میندازه تو بکگراند و به صورت deamon اجراشون میکنه

```bash
systemctl [start|stop|restart|status|enable|disable|mask|unmask] [service_name]
```

با اجرای دستور `systemctl enable [service_name]` در واقع میگیم که این سرویس بعد از ریبوت اجرا شود و خود systemd با توجه به ترتیبی که در systemd file وجود دارد آن را اجرا می‌کند.
معمولا سرویس‌هایی که معتبر هستند بعد از نصب خودشون این قابلیت رو enable میکنند
هر سرویسی یک systemdfileی دارد که در آن ما میتونیم تنظیم که این سرویس بعد از چه سرویس بیاد بالا، قبل از چه سرویسی بیاد بالا، وقتی میاد بالا با چه دستوری اجرا بشه، به صورت کلی تنظیمات اون سرویس در آن فایل وجود دارد

دستور `systectl mask [service_name]` برای این استفاده میشه که وقتی ما یه سرویس رو stop کردیم، اگر کسی بخواد که اون رو دوباره اجرا کنه یه هینتی داده میشه که این سرویس mask شده، میشه با دستور unmask اون سرویس رو از حالت mask درآورد ولی به هر حال یه هینتی داده میشه که حواسمون باشه سرویس احتمالا به یه دلیلی stop شده

با دستور `systemctl edit [service_name]` میتونیم به سرویس مدنظر فایل کانفیگ systemd بدیم
به طور کلی معمولا فایل کانفیگ سرویس را ویرایش نمی‌کنن و یک فایل دیگه میسازن و با دستور edit اون فایل رو overwrite میکنن روی فایل اصلی

**بعضی از دستورات:**

`systemctl is-enabled [service_name]`: چک میکنه که این سرویس enable برای اجرا بعد از ریبوت هست یا خیر

``

### journald

این سرویس در لینوکس این امکان رو به ما میده که لاگ اون یونیتی که داریم باهش کار می‌کنیم رو ببینیم

``` bash
journalctl
```

```
journalctl -xefu nginx
```


***نکته:***
هر کار یا دستوری که در لینوکس اجرا کردین، حتما بعدش تست کنید یا یه ولیدیشن انجام بدین که ببینین اون دستور درست اجرا شده یا نه



### virtual memory
لینوکس virtual memory را ساپورت می‌کند، به این صورت که آن قسمت‌هایی از مموری که الان استفاده نمیشن و مموری رو اشغال کردند میاره روی دیسک خودش و وقتی پراسسی دوباره به آن قسمت‌ها نیاز داشت، آنها رو میاره روی مموری
virtual memory vs swap:
در swap ما انگار داریم یه دیسک اضافه می‌کنیم به مموری، و وقتی مموری پر شد میاد روی swap
ولی در virtual memory وقتی یک پراسس به اصطلاح idle میشه میاره روی دیسک


### virtualization
با virtualization می‌تونیم تیکه تیکه منابع رو جدا کنیم و روی آنها سیستم عامل بیاریم بالا و باهشون کار انجام بدیم
قبل از virtualization فرآیند به این شکل بود که یه سرور فیزیک تهیه میشد با منابع مشخص، بعد روی آنها پراسس‌های لازم رو اجرا می‌کردیم و معمولا به این شکل بود که نمیشد از تمام منابع سرور استفاده کنیم، یا اگر استفاده میکردیم خیلی سرور شلوغی میشد

به نرم‌افزاری که اون وسط قرار میگیره و این virtualization رو برای ما انجام میده میگیم hypervisor

#### انواع virtualization

 ۱ - bear metal virtualization: در این از مجازی‌سازی ترتیب لایه‌ها به صورت زیر است

hardware
hypervisor
VMs (RAM, CPU, HARD)
OS
اصطلاحا به این مجازی‌سازی می‌گن VM (virtual machine)
در کلاد پرووایدرهای مختلف به این vmها اصطلاحات مختلفی میگن، مثلا در آروان میگن ابرک، در زبان openstack میگن instance، یا در digital ocean بهشون میگن droplet

۲ - container: این مجازی‌سازی در سطح سیستم عامل انجام می‌شود، ما می‌توانیم یک کرنل share داشته باشیم و پراسس‌هامون رو ببریم داخل یک محیط کاملا ایزوله و با یه منابع کاملا مشخص اجراشون بکنیم

۳ - hosted: در این نوع مجازی‌سازی با استفاده از ابزارهایی مثل virtualbox یا vmware که روی سیستم عامل نصب میشن، می‌توان یک محیط مجازی داشته باشیم


***نکته:*** hypervisor خانواده vmware ابزاری به نام ESXI هستش، ابزار vcenter یک ابزاری هست که بالای سر همه hypervisorها استفاده میشه و میتونه اونها رو باهم کلاستر بکنه



## booting process
#### [[BIOS]] (basic input output system)
در فرآیند بوت لینوکس، در ابتدا bios میاد بالا و یک initialize خیلی کوچک از سخت‌افزار انجام می‌دهد، در نسخه‌های جدیدتر اسمش [[UEFI]] هستش، یک محیط گرافیکی هم در اختیار کاربر میزاره
معمولا bios و UEFI روی یک رامی توی motherboard ذخیره میشن که جدای از disk اصلی هستش
در کانفیگ این bios میگیم که از روی چه دیسکی باید سخت‌افزار بوت بشه

#### [[boot loader]]
بعد از اینکه bios کارش تموم شد، boot loader میاد که وظیفه مهمی به عهده داره
boot loader در سکتورهای اول هارد میشینه
کارش اینکه [[kernel]] رو لود کنه
یکی از معروف‌ترین و محبوب‌ترین boot loaderها اسمش [[GRUB]] هستش که الان نسخه ۲ اون رو داریم استفاده می‌کنیم
از دیگر boot loaderها می‌توان به [[LILO]] هم اشاره کرد

کلا بوت لودرها دو تا کار انجام میدن، اول اینکه کرنل رو توی رم لود میکنن و پارتیشنی که باید لود بشه رو صدا میزنه، در grub شما می‌تونید کانفیگ کنید و چندین کرنل رو ساپورت بکنید و بوت بکنید، یا اصطلاحا [[dual boot]] بکنیم

گاهی اوقات پیش میاد که پسورد سرور رو نداریم، میتونیم از طریق grub بریم اون پارتیشنی که داریم رو لود بکنیم و پسورد رو عوض کنیم

گاها روی grub پسورد میزارن ولی کار سختی هستش چون وقتی سرور ریبوت بشه، باید اون پسورد رو بزنیم
در پروداکشن معمولا این کار رو نمیکنن

بعد از اینکه بوت لودر کرنل رو لود کرد، کرنل هم چند کار مهم داره، یکی initialize سخت‌افزار هستش، سخت‌افزار رو کلا تست میکنه، verification انجام میده
بعدش میاد سراغ اینکه پارتیشن‌ها رو برداره، در واقع مسیر `/` رو لود میکنه، بعدش systemd رو میاره بالا که systemd خودش شروع میکنه سرویس‌ها رو میاره بالا


در ادامه میخوایم راجع به [[Disk]] در لینوکس صحبت بکنیم