Linux supports _virtual memory_, that is, using a disk as an extension of RAM so that the effective size of usable memory grows correspondingly. The kernel will write the contents of a currently unused block of memory to the hard disk so that the memory can be used for another purpose. When the original contents are needed again, they are read back into memory.

Virtual memory is a combination of RAM and disk space that running processes can use. **Swap space** is the **portion of virtual memory** that is on the hard disk, used when RAM is full.

![[Pasted image 20240715085022.png]]

![[Pasted image 20240715085107.png]]

در virtual memory کرنل هر موقع نیاز پیدا کرد پراسس رو میبره روی دیسک، ولی در swap انتهای ظرفیت RAM میره روی دیسک
![[Pasted image 20240715085327.png]]

![[Pasted image 20240715085259.png]]


## check memory usage using the CLI and GUI

CLI:
`/proc/meminfo`
`free`
`vmstat`
`top`
`atop`
`htop`
`sar`
`btop`

GUI:
Gnome System Monitor


``` bash
cat /proc/meminfo
less /proc/meminfo
more /proc/meminfo
grep -E --color 'Mem|Cached|Swap' /proc/meminfo
```

the `/proc/meminfo` file contains many more values that may be relevant for system monitoring and troubleshooting tasks. You can use tools like `grep` or `awk` to focus your search on specific metrics.

![[Pasted image 20240715124257.png]]

![[Pasted image 20240715125121.png]]
![[Pasted image 20240715124821.png]]

![[Pasted image 20240715125153.png]]


![[Pasted image 20240715130136.png]]
در کامند `htop` یه بخشی داریم به نام load average که به ازای هر cpu یه عدد بالاتر می‌رود، یعنی اگر ما 16 core cpu داشته باشیم، وقتی این مقدار 16 هستش، یعنی cpu من داره ۱۰۰ درصد استفاده میشه
معنیش هم این هستش که تعداد پراسس‌هایی که نیاز به cpu دارند و در صف قرار گرفتند تا cpu تایم بهشون برسه

![[Pasted image 20240715131425.png]]


یک نکته در مورد swap:
ابزارهای جدید با swap زیاد حال نمیکنن، چرا؟ چون بهتره که وقتی تو رم سرورت پر شده به منیجر بالا دستیش بگه که رمم پر شده تا job جدید بهش نده، نه اینکه ببره روی دیسک و باعث کندی اون بشه


![[Pasted image 20240715132027.png]]


