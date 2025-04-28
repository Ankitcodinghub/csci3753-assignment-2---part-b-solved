# csci3753-assignment-2---part-b-solved
**TO GET THIS SOLUTION VISIT:** [CSCI3753 Assignment 2 – Part B Solved](https://www.ankitcodinghub.com/product/csci3753-pa2-part-b-solved/)


---

📩 **If you need this solution or have special requests:** **Email:** ankitcoding@gmail.com  
📱 **WhatsApp:** +1 419 877 7882  
📄 **Get a quote instantly using this form:** [Ask Homework Questions](https://www.ankitcodinghub.com/services/ask-homework-questions/)

*We deliver fast, professional, and affordable academic help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;118654&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;2&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (2 votes)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CSCI3753 Assignment 2 - Part B Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (2 votes)    </div>
    </div>
&nbsp;

Introduction

In this assignment we will explore file I/O and how to implement a basic device driver inside a Loadable Kernel Module (LKM). First, you will write a user-space C program that takes commands from the user to read, write and seek on a file. You will use this program to test the functionality of a custom device driver that you’ll create in Part B.

Part B – Device Driver LKM

Linux Devices Overview

In Linux, device I/O is modeled using files. Reading from and writing to a file will invoke the associated device driver to do the actual reading and writing. All device drivers have a major and a minor number, where the major number is unique to every device driver. The minor number differentiates all the devices belonging to that device driver.

For example, a typical system will have multiple hard disks, or at least multiple partitions on a single disk. A single major number is used to specify the hard disk device driver, but each partition has a different minor number. If you type ls –l /dev/sda* on your VM, this will show all the device files associated with all the hard disk partitions. You should see the partitions listed with their corresponding major and minor numbers:

It’s worth noting that there are two kinds of device drivers:

A character device driver reads and writes from/to the device character by character. This is the most basic type of device driver and usually the simplest to implement.

A block device driver reads or writes large chunks (blocks) of data with a single read/write operation.

These types of drivers are more complex, but usually more efficient in their use of system resources.

Network interfaces and disk controllers generally prefer to use a block driver.

Many devices will have both a character and a block driver available. It’s then up to the application programmer to decide which is the most appropriate or convenient to use.

Creating A Device File

To access your device driver, you will need to create a corresponding device file in the /dev directory, using the command mknod:

sudo mknod -m &lt;permission&gt; &lt;device_file_location&gt; &lt;type of driver&gt; &lt;major number&gt; &lt;minor number&gt;

For example, sudo mknod -m 777 /dev/simple_character_device c 240 0 creates a device file where:

-m 777 sets the permission so that all users can read, write and execute the file simple_character_device is the name of the device file c specifies the type of driver, in this case a character driver

240 is the major number of the driver that will be associated with this device file 0 is the minor number of the device

The major number you choose for your driver must be unique. Inside your Linux source tree, in the file /home/kernel/linux-hwe-4.15.0/Documentation/admin-guide/devices.txt , check for the current device drivers and their associated major/minor numbers.

Device Driver Overview

The diagram below summarizes what is going on when you are working with a device driver. From a userspace program, you will issue calls to open(), read(), write(), seek() or close() . These calls will access the device file in /dev which is associated with your device driver.

For example, when you run echo hello &gt;file.txt , the operations performed are: open the file, write “hello” to the file, and then close the file.

Similarly, when you run the command cat file.txt , the operations performed are: open the file, read the file content, and then close the file.

The device file, by way of its major and minor numbers, indicates to the kernel that you are trying to perform file operations on a device. The kernel will invoke the corresponding file operations in the device driver. The device driver then executes it’s implementation of these file operations against the physical device.

For the purposes of this assignment, our device driver will only read and write data to a region of memory instead of an actual physical device.

Device Driver Implementation

Along with the header files necessary for module programming, you’ll also need to include: linux/fs.h – contains the functions that are used to manipulate files

linux/uaccess.h – enables you to access data from user-space in the kernel and vice versa

Declare your init() and exit() functions and use module_init() and module_exit() to bind these functions

In your init() function, register your character driver using register_chrdev()

In your exit() function, unregister the driver using unregister_chrdev()

register_chrdev() takes three parameters: major number, a unique name, and a pointer to a file operations struct (see below). Check google or the references section of this writeup for questions regarding register_chrdev() and unregister_chrdev() .

We will use a dynamically allocated kernel buffer (hereby referred to as device_buffer ) with a fixed size to store the data written to our device. You should allocate memory for this buffer at initialization time and free this memory before exiting. There are two core functions to manage memory in the Linux kernel defined in &lt;linux/slab.h&gt;:

void* kmalloc(size_t size, gfp_t flags) allocates memory for use in the kernel, use the macro GFP_KERNEL as the flags argument in this case

void kfree(const void* kptr) frees memory previously allocated using kmalloc()

Make sure you use a constant or macro to set the size of this buffer to 1KiB.

Device File Operations

To perform file operations in your device driver you need to populate a file_operations structure. The system defined struct is found in /lib/modules/$(uname –r)/build/include/linux/fs.h . Create a similar structure with the same struct file_operations type but with a different name. Define the open(), close(), seek(), read() and write() operations only. You will have to implement these five functions, and set the function pointers in your file_operations struct to point to your implementations. Note that there is no ‘close’ function in the file_operations struct, use release() instead.

You are free to use the example below, the comments describe the interface your functions must implement:

struct file_operations my_file_operations = {

.owner = THIS_MODULE,

.open = my_open, // int my_open (struct inode *, struct file *);

.release = my_close, // int my_close (struct inode *, struct file *);

.read = my_read, // ssize_t my_read (struct file *, char __user *, size_t, loff_t *);

.write = my_write, // ssize_t my_write (struct file *, const char __user *, size_t, loff_t *);

.llseek = my_seek // loff_t my_seek (struct file *, loff_t, int); };

Open – The open function takes two parameters, a pointer to an inode struct (which represents the physical file on the hard disk), and a pointer to a file struct (represents the state of a file), and returns an integer indicating success or failure. In this function, you don’t need to do anything other than log the number of times the device has been opened.

Release – The release function takes the same two parameters as open() and again returns an integer indicating success or failure. Use printk() to output the number of times the device has been closed.

Read – The read function expects four parameters: a file pointer, a pointer to a user-space buffer, the size of that buffer, and a pointer to the current position. Use the function copy_to_user() to copy data from the device_buffer, starting at the current position, to the user-space buffer. If successful, make sure to update the current position, and then return the number of bytes read. Use printk() to log the number of bytes read.

Seek – The seek function takes three parameters, a file pointer, an offset, and the value whence. Whence describes how to interpret the offset (note that offset can be negative). If the value of whence is 0 ( SEEK_SET) , the position is set to the value of the offset. If the value of whence is 1 (SEEK_CUR) , the current position is incremented (or decremented, if negative) by offset bytes. Finally, if the value of whence is 2 ( SEEK_END) , the position is set to offset bytes from the end of the file.

If a user attempts to read, write or seek before the beginning or beyond the end of the device_buffer, an error should be indicated by returning a -1, and the current position should be left unchanged.

You will need to implement some sort of bounds checking to ensure this behavior.

To get you started, we’ve provided a skeleton of these functions here.

Install and test the Module

Follow the instructions from PA1 to compile and install your LKM. Verify that it’s installed by checking the kernel log for printk() output, lsmod, or by looking in /proc/devices. Try to echo into (write) and cat from (read) your device file, or better yet, use your test program from Part A.

Submission

You are required to submit the following to Canvas:

pa2_char_driver.c

We will also look at your CloudVM to determine if you successfully compiled and installed this module
