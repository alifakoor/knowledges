فایل‌هایی که برای userها و groupها در لینوکس مهم هستند:
`/etc/shadow`  secure user account information
`/etc/passwd` user account information
`/etc/gshadow` contains the shadowd information for group accounts
`/etc/group` defines the group to which users belong
`/etc/sudoers` configuration for sudo

**نکته:**
حتما برای ویرایش فایل `/etc/sudoers` از پلاگین `visudo` ویرایشگر vim استفاده کنید، بابت اینکه اگر این فایل را اشتباه کانفیگ کنید باعث میشه که دسترسی root هم دچار مشکل بشه و دیگه نتونین کاری بکنید
این پلاگین یه قابلیتی میده که اگر سینتکس فایل اشتباه باشه، ذخیره نشه

**ساختار یک خط از فایل passwd:**

![[Pasted image 20240729160418.png]]

**ساختار یک خط از فایل group:**

![[Pasted image 20240729160557.png]]


### PAM (pluggable authentication modules)
یک ماژول که به وسیله اون میتونیم به یک authentication مرکزی وصل بشیم
یکی از مثال‌های این ابزارهای authentication مثلا [FreeIPA](https://www.freeipa.org/) هستش یا مثلا [OpenLDAP](https://www.openldap.org/)


### sudo and sudoer file
ابزار sudo این امکان رو به ما میده که بیایم یک کامندی رو با پرمیژن بالاتری انجام بدیم
معمولا اینطوری نیست که با یوزر root یه کاری رو انجام بدن، با همون یوزر خودشون این کار رو انجام میدن و اگر نیاز شد از sudo استفاده میکنن
فایل `/etc/sudoers` این امکان و کانفیگ رو به ما میده که بگیم کدوم یوزرها sudoer باشند و اینکه مثلا با پسورد لازمه که sudo اجرا کنه یا نه، حتی میتونیم بگیم که کاربر چه کامندهایی رو با sudo بتونه بزنه
این فایل، فایل خیلی حساس و مهمیه، برای همین همینطوری این فایل رو ویرایش نکنید، حتما از پلاگین visudo برای ویرایش این فایل استفاده کنید
این فایل حتی برای یوزر root هم به صورت پیش‌فرض فقط قابلیت read دارد و اگر بخواهید write کنید باید خودتون پرمیژن بدین

check sudo command logs:
```sh
journalctl -f SYSLOG_INDENTIFIER=sudo
```

**ساختار یک خط از فایل sudoers:**
![[sudoers-syntax.png]]

کانفیگ NOPASSWD برای این هستش که مشخص کنیم کاربر میتونه کدوم کامندها رو بدون پسورد بزنه، البته این خوب نیست و بهتر هستش که پسورد بگیریم از کاربر

بهتر هستش که خود فایل `/etc/sudoers` رو تغییر ندیم و مثلا یه فایل به نام کاربر در مسیر `/etc/sudoers.d/ali` بسازیم و کانفیگ اون یوزر رو تو اون بزاریم که فایل اصلی هم مشکلی براش پیش نیاد


### Commands:
`adduser`
`userdel`
`addgroup`
`delgroup`
`passwd` change user password
`usermod` modify a user account
`chage` change user password expiry information
`newgrp` log in to a new group

`finger` get details about user
`id` print real/effective UIDs/GIDs and tells user belong to which groups
`last` show listing of last logged in users
`su` start a new process as a different user
`sudo` execute a command as a different user
`users` show who is logged on
`w` show logged-in users and their current tasks
`who` show who is logged on
`whoami` show who is logged on
`write` send a message to another user

**نکته:**
معمولا برای آدم‌های مختلف در سرور یوزر مربوط به خودشان را میسازیم تا بعدا اگر اتفاقی افتاد اینطوری نشه که نتونیم پیدا کنیم کسی رو که اون کار رو کرده



