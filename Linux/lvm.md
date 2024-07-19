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

1. **Creating a Physical Volume**:
    ```sh
    pvcreate /dev/sdX
    ```

2. **Creating a Volume Group**:
    ```sh
    vgcreate my_volume_group /dev/sdX1 /dev/sdX2
    ```

3. **Creating a Logical Volume**:
    ```sh
    lvcreate -L 10G -n my_logical_volume my_volume_group
    ```

4. **Resizing a Logical Volume**:
    - To extend:
        ```sh
        lvextend -L +5G /dev/my_volume_group/my_logical_volume
        ```
    - To reduce (after reducing the filesystem first):
        ```sh
        lvreduce -L -5G /dev/my_volume_group/my_logical_volume
        ```

5. **Creating a Filesystem on a Logical Volume**:
    ```sh
    mkfs.ext4 /dev/my_volume_group/my_logical_volume
    ```

6. **Mounting a Logical Volume**:
    ```sh
    mount /dev/my_volume_group/my_logical_volume /mnt/my_mount_point
    ```

### Example Workflow:

1. **Initialize Physical Volumes**:
    ```sh
    pvcreate /dev/sda1 /dev/sdb1
    ```

2. **Create a Volume Group**:
    ```sh
    vgcreate my_vg /dev/sda1 /dev/sdb1
    ```

3. **Create a Logical Volume**:
    ```sh
    lvcreate -L 20G -n my_lv my_vg
    ```

4. **Create a Filesystem on the Logical Volume**:
    ```sh
    mkfs.ext4 /dev/my_vg/my_lv
    ```

5. **Mount the Logical Volume**:
    ```sh
    mount /dev/my_vg/my_lv /mnt/my_data
    ```

6. **Resize the Logical Volume**:
    ```sh
    lvextend -L +10G /dev/my_vg/my_lv
    resize2fs /dev/my_vg/my_lv
    ```

Using LVM, you can efficiently manage disk storage in a flexible and scalable way, making it a powerful tool for system administrators.


