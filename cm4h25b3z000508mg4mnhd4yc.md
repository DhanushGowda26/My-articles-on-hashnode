---
title: "Understanding Storage and LVM"
datePublished: Mon Dec 09 2024 13:17:51 GMT+0000 (Coordinated Universal Time)
cuid: cm4h25b3z000508mg4mnhd4yc
slug: understanding-storage-and-lvm
tags: aws, azure, devops, storage

---

In the world of system administration and DevOps, effective management of storage resources is essential for maintaining smooth and efficient operations. From basic partitioning to advanced Logical Volume Management (LVM), understanding how to work with storage at a low level is crucial for any system administrator or DevOps engineer. In this blog, I’ll walk through the essential concepts, starting with basic disk partitioning and moving toward more advanced techniques like LVM.

### Understanding Disk Partitioning: MBR vs GPT

Disk partitioning is the process of dividing a physical disk into multiple logical sections, each known as a partition. Partitions allow the operating system to manage disk space and separate data. While there are multiple ways to partition a disk, the most commonly used are **MBR (Master Boot Record)** and **GPT (GUID Partition Table)**.

#### **MBR (Master Boot Record)**

* MBR is the older partitioning scheme that dates back to the 1980s. It is still commonly used on older systems and disks.
    
* **Limitations of MBR**:
    
    * Can support up to 4 primary partitions (or 3 primary and 1 extended partition).
        
    * Maximum disk size supported is 2TB.
        
    * Limited to using the legacy BIOS boot system.
        

#### **GPT (GUID Partition Table)**

* GPT is the modern partitioning scheme designed to replace MBR. It is a part of the UEFI (Unified Extensible Firmware Interface) standard, which replaces BIOS in modern systems.
    
* **Advantages of GPT**:
    
    * Supports disks larger than 2TB.
        
    * Allows more than four primary partitions (up to 128 partitions on most systems).
        
    * More robust and offers better data integrity with CRC checks on partition tables.
        

**GPT** is the preferred partitioning style for modern systems, especially if you are dealing with large disks or need more than four partitions. It also works well with UEFI systems, which are becoming more standard in new hardware.

---

### BIOS vs UEFI: Which One Should You Use?

When setting up your disk or operating system, you will also encounter the terms **BIOS (Basic Input/Output System)** and **UEFI (Unified Extensible Firmware Interface)**. These are the firmware interfaces that initialize hardware and start the operating system.

#### **BIOS**

* BIOS is the older standard, still widely used in many older systems.
    
* It operates in 16-bit mode, which limits its capability.
    
* BIOS systems can only boot from MBR partitioned disks.
    

#### **UEFI**

* UEFI is the modern replacement for BIOS, offering better performance, security, and flexibility.
    
* It supports booting from GPT-partitioned disks.
    
* UEFI allows faster boot times and more advanced features like Secure Boot and better hardware compatibility.
    

As modern operating systems and hardware are designed for UEFI, it is generally recommended to use UEFI over BIOS for newer systems, especially when dealing with large storage devices.

---

In Azure I had done hands-on by attaching a new disk to vm

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733744653395/dff08eb1-3bed-480b-ba9b-a75149cf5f50.png align="center")

This is how it looks initially, while booting it will create a partition for all its operations and here sda1 is what we use normally

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733744666764/74797c1b-e16c-477a-9206-855241981ecd.png align="center")

In Linux, devices like hard drives and partitions are assigned to files in the `/dev/` directory.

In Linux, `/dev/root` is a symbolic reference to the root filesystem of the system, which is the primary filesystem that contains the operating system and all other files. It's essentially the filesystem where the root directory (/) is located.

when attached new disk of size 4Gb

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733744807766/cb5f7ce7-497f-47e2-becf-6bda4c6872c7.png align="center")

her, sdc is the attached disk now we need to partion and mount so that, we cau use

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733745006103/0f28b74d-e37e-4a72-a796-f64a25f78b87.png align="center")

out of available 4gb, created partion of 2gb

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733745103412/dc606a22-cf7d-4f23-8c7c-cadd9bfeba04.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733745264142/2f089022-021f-4bc1-8d04-d599da94efa5.png align="center")

The command `sudo mkfs.ext4 /dev/sdc1` is used to format the partition `/dev/sdc1` with the `ext4` file system.

### What it does:

* **Wipes existing data**: Formatting the partition with `mkfs.ext4` erases any data that may already exist on the partition.
    
* **Creates an ext4 filesystem**: It initializes the partition with the ext4 filesystem structure, which includes inodes, data blocks, superblocks, etc. This makes the partition ready to store files in the ext4 format.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733745364307/59b62b12-ea56-411b-8e36-95be25f76a39.png align="center")

now we can create another partion or add 2gb to the allready existing partion to do this 2nd option you need delete and recreate the partion and there is a risk of loosing data as we are deleting partion is involoved.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733746534727/805d92ae-f6df-4cef-a0b9-ae315a98f3ba.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733746708389/e3d3eca9-c2de-42e3-ab07-ca246820f708.png align="center")

Now we will unmount and use LVM

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733746972615/6936b627-a73e-4958-8184-1480f5a9e856.png align="center")

The **signature** on a disk or partition is essentially metadata that indicates which type of filesystem or partitioning scheme is being used. This information is stored in a specific part of the disk (usually the beginning) and helps the operating system identify how the disk or partition is structured.

When you run `sudo wipefs /dev/sdc1`, you are removing these signatures, which means:

1. **Filesystems like ext4, NTFS, or others**: These partitions have metadata that the operating system uses to understand how the data is organized (e.g., where the file system starts and ends, how files are indexed, etc.). If you wipe the signature, the partition is no longer recognized as a valid filesystem.
    
2. **Partition Tables like MBR or GPT**: These partition tables also have signatures that describe how the disk is divided (which part is for the OS, which part is for data, etc.).
    

### What Happens When You Keep the Signature:

* If you keep the signature, the partition will still be recognized as having the original filesystem, and the data in it may still be accessible if the filesystem isn't corrupted. You can mount the partition, and the operating system will know how to read the data stored on it.
    

### To Preserve Data:

If you want to preserve the data:

1. **Backup the data** before wiping the signature.
    
2. Alternatively, if you're just planning to use the partition for LVM or another system, you can **move the data** off the partition, wipe the signature, and then create the new system on the partition.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733747369978/487ae00c-cc10-4a04-998f-e28604e92b4e.png align="center")

so here volume group is a collection of disk partions and using that we create logical volume

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733748427420/e9c1c4ce-19b6-438b-a008-d7829bad4046.png align="center")

You can both **create multiple volume groups (VGs)** and assign multiple logical volumes (LVs) to them, or **create a single volume group** and assign multiple logical volumes to it. The choice depends on how you want to organize and manage your storage.

### Here's what you should do if you want to add a new partition to LVM:

1. **Create a new partition** using a tool like `fdisk` or `parted` (e.g., `/dev/sdc`).
    
2. **Create a Physical Volume (PV)** using the new partition:
    
    ```plaintext
    sudo pvcreate /dev/sdc3
    (or)
    sudo pvresize /dev/sda3 #if incread size of existing
    ```
    
3. **Add the PV to an existing Volume Group (VG)**:
    
    ```plaintext
    sudo vgextend my_volume_group /dev/sdc3
    ```
    
4. **Extend a Logical Volume (LV)** within the VG:
    
    ```plaintext
    lvextend -l +100%FREE /dev/my_volume_group/my_logical_volume
    ```
    
5. **Resize the filesystem** on the LV:
    
    * For ext4:
        
        ```plaintext
        sudo resize2fs /dev/my_volume_group/my_logical_volume
        ```
        

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733749552819/72cf263f-2896-4dff-b62b-346b6a6e1ed2.png align="center")

In the above case, let say sda disk increased to 86 and you need to increase, so here sda3 is a part of lvm, so here, instead of creating new partion sda4, you can delete sda3 and and craete it back with available free size and also dont remove signature and then extend lvm.

**Do not remove the signature**: As long as you don't remove the signature (by formatting or using `wipefs`), the data on `/dev/sda3` should remain intact.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733749270606/61b349c6-0880-46ee-8e24-05fa240d5134.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733749271364/25779a50-7c03-4fa5-b8ec-a73c88c71b43.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733749449875/be6864d8-f4a3-4924-bed3-da62aea05fd7.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1733749672268/4a40dee1-8162-495d-8c77-384b3c609763.png align="center")

Thank You