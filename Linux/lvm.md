LVM, Logical Volume Management

اگر شما یک دیسک داشته باشی که از اون در لینوکست استفاده کنی، دیگه نمیتونی فضای اون دیسک رو بیشترش کنی، مثلا اگر یه دیسک ۳۰ گیگی داری، و یه دیسک دیگه میگیری ۴۰ گیگ، دیگه نمیتونی این ۴۰ گیگ رو اضافه کنی به اون ۳۰ گیگ، دیگه نمیتونی مثلا دو تا مسیر `/` داشته باشی، مگر اینکه مثلا بیای mount pointها رو عوض کنی، مثلا بیای مسیر `/var` رو بجای اینکه توی دیسک ۳۰ گیگی بمونه، بیای mountش کنی روی اون دیسک ۴۰ گیگی، مگر اینکار رو بکنی که فضای اون دیسک ۳۰ گیگی خالی بشه، بازم در این حالت تو فضای اون دیسک رو بیشترش نکردی، بلکه فضا خالی کردی
حالا lvm اومده این مشکل رو حل کنه

Logical Volume Management (LVM) in Linux is a system for managing disk storage that provides more flexibility compared to traditional partitioning. Here are the key concepts and components:

### Key Concepts:

1. **Physical Volumes (PVs)**: These are the actual storage devices, such as hard drives or partitions, that are used in LVM. You can think of them as the raw storage.
    
2. **Volume Groups (VGs)**: A volume group is a collection of physical volumes. By combining multiple physical volumes into a single volume group, LVM can treat them as a single pool of storage.
    
3. **Logical Volumes (LVs)**: Logical volumes are created from the space within a volume group. They are analogous to traditional partitions, but they can span multiple physical volumes within the volume group. This provides greater flexibility in managing storage.
    

### Benefits of LVM:

1. **Dynamic Resizing**: You can easily resize logical volumes as needed without having to unmount file systems or repartition disks.
    
2. **Flexibility**: Logical volumes can span across multiple physical volumes, which allows you to create larger volumes than the size of a single physical disk.
    
3. **Snapshots**: LVM supports the creation of snapshots, which are read-only copies of a logical volume at a given point in time. This is useful for backups and consistent state captures.
    
4. **Improved Disk Space Management**: You can allocate storage more efficiently, expanding or reducing volumes as required without much hassle.

![[basic-lvm-volume_0.png]]


![[Pasted image 20240719221314.png]]


lvm structure:

![[lvm.webp]]

![[lvm-levels.jpg]]


### Basic LVM Commands:

list block devices:
```sh
lsblk
```

show volume group:
``` sh
sudo vgs
```

show information about logical volumes:
```sh
sudo lvs
```


حالا میخوایم یه سناریو باهم پیش ببریم:
اگر دستور `lsblk` رو بزنیم خروجی مثلا به شکل زیر هستش:

![[Pasted image 20240720201023.png]]

حالا فکر کنید اون دیسک 64 گیگیمون پر شده و میخوایم که اون دیسک sdb که ۲۵ گیگ هستش رو به اون اضافه کنیم و بشه 89 گیگ، بریم که باهم داشته باشیم:
اولین کاری که میکنیم پارتیشن‌بندیه
```sh
sudo fdisk /dev/sdb
```
*مراحل مربوط به پارتیشن‌بندی را انجام میدهیم


show physical volumes:
```sh
sudo pvs
```

میتونیم یک physical volume بسازیم
اما میتونیم یک volume group بسازیم و پیش فرض خودش physical volume هم میسازه
برای ساختنش از دستور زیر استفاده می‌کنیم:
```sh
vgextend [volume_group_name] [partition_that_you_want_to_add]
```


