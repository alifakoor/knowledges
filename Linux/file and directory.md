کلا فایل‌ها تو لینوکس خیلی مهمه، چون تو لینوکس همه چی فایله
دو تا دستور مهم داریم:
`chown` change the owner of file
`chmod` change the file mode

`lsattr` list of file attributes
`chattr` change file attributes

در لینوکس می‌تونیم برای فایل‌ها و دایرکتوری‌ها attributeهای مختلف داشته باشیم، از attributeهای معمول میشه به موارد زیر اشاره کرد:
`a` - append only: file can only be opened for appending
`c` - compressed: enable filesystem-level compression for the file
`i` - immutable: cannot be modified, deleted, renamed, linked to. can only be set by root
`j` - data journaling: use the journal for file data writes as well as metadata
`m` - no compression: disable filesystem-level compression for the file
`A` - no atime update: the file's atime will not be modified
`C` - no copy on write: disable copy-on-write, for filesystems that support it

به صورت پیش‌فرض فایل‌ها attribute e دارند که میشه ادیت

برای مثال برای اضافه کردن attribute a میتونیم از دستور زیر استفاده کنیم
`chattr +a [file_name]`

**داخل پرانتز:**
یکی از فرق‌های printf و echo این است که echo انتهای عبارت یک enter میزنه و میاد خط بعدی، ولی printf این رو نداره، برای اینکه echo هم enter نزنه، میتونیم از اپشن -n استفاده کنیم:‍ `echo -n ali`

**نکته:**
یکی از کاربردهای attribute i این هستش که شما وقتی بکاپ میگیری از سرورت، بیای اون فایل‌های بکاپ رو immutable کنی تا یوزرها دیگه نتونن ادیتش کنن یا پاکش کنن، این کجا کاربرد داره؟ جایی که شما مورد حمله [[ransomware]] قرار گرفتی، تو این حمله، مهاجم میاد همه فایل‌های شما رو انکریپت میکنه و باج میخواد تا فایل‌هاتون رو برگردونه، اما اگر شما فایل‌های بکاپتون رو immutable کنید، دیگه نمیتونه اونها رو ادیت کنه و میتونین اگر دچار این حمله شدید، از روی بکاپ، فایل‌هاتون رو برگردونین

### file and directory access

read, write and execute premissions

![[Pasted image 20240731115551.png]]

![[Pasted image 20240731115838.png]]

**نکته:**
لینوکس به صورت پیش‌فرض پرمیژن 644 رو به فایل‌ها و دایرکتوری‌ها میده، که این مقدار پیش‌فرض رو هم میشه کانفیگ کرد تا به صورت پیش‌فرض یه پرمیژن دیگه بده به فایل‌ها و دایرکتوری‌ها

![[Pasted image 20240731120234.png]]

![[Pasted image 20240731120727.png]]

فایل تایپ‌هایی که وجود دارد:
`-` : regular file
`d`: directory
`c`: character device file
`b`: block device file
`s`: local socket file
`p`: named pipe
`l`: symbolic link

**sticky bit:**
اگر بخواهیم یک فایلی رو بسازیم که اجازه deleteش فقط برای اون کاربری باشه که ساختتش، میتونیم از sticky bit استفاده کنیم، که اخر اون بخش پرمیژن‌ها یه t میزاره، برای اینکه این رو به یک فایل بدیم از دستورات زیر میتونیم استفاده کنیم:
```sh
chmod o+t [file_name]
or
chmod +t [file_name]
or
chmod 1757 [file_name]
```

chmod options;
![[Pasted image 20240731122557.png]]


### Link

In your linux file system, a link is a connection between a file name and the actual data on the disk. there are two main types of links that can be created: 
hard link
soft link or symbolic link

تفاوت soft link و hard link:
در soft link خود لینک هیچ ماهیتی نداره و تمام محتوا از روی فایل اصلی میاد، و اگر فایل اصلی پاک بشه، soft link هم از بین میره
برای ساخت soft link میتونیم از دستور زیر استفاده کنیم:
```sh
ln -s [main_file] [link_file_name]
```

اما در hard link انگار که یه فایل دیگه میسازه از روی فایل اصلی و بهم لینکشون میکنه، چون اگر در فایل اصلی تغییری ایجاد بشه تو این فایل هم تغییر ایجاد میشه و برعکس، همچنین اگر فایل اصلی پاک بشه، این فایل باقی‌میمونه
برای ساخت hard link میتونیم از دستور زیر استفاده کنیم:
 ```sh
 ln [main_file] [link_file_name]
```

یکی دیگه از تفاوت‌های آنها این هست که در ساخت hard link ما inode مصرفی نداریم

 ![[Pasted image 20240731123936.png]]
![[Pasted image 20240731124022.png]]


از تفاوت‌های کپی و hard link هم میتوان به این اشاره کرد که inode مصرفی نداریم در hard link و اینکه اگر فایل اصلی تغییر بکنه فایل hard link هم تغییر میکنه و بالعکس، که در این کپی این موارد رو نداریم

 