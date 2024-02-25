# Implementing Wordpress Website with LVM Storage Management

Welcome to implementing wordpress website with LVM Storage Management on AWS EC2 Redhat course. If you are eager to learn how to implement wordpress website with LVM Storage Management on AWS EC2 then this course is for you. This course takes you through step by step implemetaion of wordpress website with LVM Storage Management using Redhat as the operating system.

## Course Objectives

By the end of this project, you would have gained the requisite knowlwdge listed below:

* Develeop the knowledge and skills to succesfully implement and manage a wordpress website on AWS EC2 using the LVM Storage Management.

* Whether you are aspiring to be a website developer, a system administrator or a Devops professional, you will learn to leverage the power of AWS cloud infrastructure to build scalable and reliable wordpress sites.

* You will learn how to create logical volumes, manage disk space and dynamicallly adjust volumes to accommodate changing storage requirements.

* You will gain the proficiency to install and configure wordpress, install themes and add essential plugins to enhance your website's functionality.

* You will learn performance optimization techniques and best practices for securing your Wordpress installation on the AWS cloud.

## Understanding 3 Tier Architechture
### Web Solution with Wordpress

![alt text](images/Wordpress.png)

WordPress is a content management system (CMS) that allows you to host and build websites. WordPress contains plugin architecture and a template system, so you can customize any website to fit your business, blog, portfolio, or online store.

It is a free and open-source content management system written in PHP and paired with MySQL or MariaDB as its backend Relational Database Management System (RDBMS).

This project consists of two parts:

 * Configure storage subsystem for Web and Database servers based on Linux OS. The focus of this part is to give you practical experience of working with disks, partitions and volumes in Linux.

* Install WordPress and connect it to a remote MySQL database server. This part of the project will solidify your skills of deploying Web and DB tiers of Web solution.

As a DevOps engineer, a deep understanding of core components of web solutions and the ability to troubleshoot them will play essential role in your further progress and development.

### Three-tier Architecture

![alt text](images/three-tier-architecture.png)

Generally, web, or mobile solutions are implemented based on what is called the Three-tier Architecture.

Three-tier Architecture is a client-server software architecture pattern that comprise of 3 separate layers. They are:

1. Presentation Layer (PL): This is the user interface such as the client server or browser on your laptop.

2. Business Layer (BL): This is the backend program that implements business logic. Application or Webserver

3. Data Access or Management Layer (DAL): This is the layer for computer data storage and data access. Database Server or File System Server such as FTP server, or NFS Server.

With this project, you will have the hands-on experience that showcases Three-tier Architecture while also ensuring that the disks used to store files on the Linux servers are adequately partitioned and managed through programs such as gdisk and LVM respectively.

**Requirements**:

Your 3-Tier Setup

1. A Laptop or PC to serve as a client
2. An EC2 Linux Server as a web server (This is where you will install WordPress)
3. An EC2 Linux server as a database (DB) server.

Note: We are using RedHat OS for this project, click on this [link](https://github.com/Psalmjoe/DevOps_Projects/tree/main/PROJECT-3) to learn how to spin up an EC2 server if you don't already know how to do so.

Also when connecting to RedHat you will need to use ec2-user user. Connection string will look like ec2-user@public-ip-address.
Implementing LVM on Linux Servers (Web and Database Servers)

### Step 1 : Prepare a Web server

1. Launch an EC2 instance that will serve as web server. Create 3 volumes of 10GiB each in the same AZ (Availability Zone) as the web server.

Learn how to attach EBS volumes to an EC2 instance [here](https://www.youtube.com/watch?v=HPXnXkBzIHw)


![alt text](<images/webserver instance.png>)

![alt text](<images/Create Volume.PNG>)

![alt text](images/volume.png)

2. Attach all three volumes one by one to your Web Server EC2 instance.

![alt text](<images/attach volume.png>)

![alt text](images/attach.png)

3. Open up the Linux terminal to begin configuration.

![alt text](<images/launch ec2.png>)

4. Use ```lsblk``` command to inspect what block devices are attached to the server. Notice names of your newly created devices. All devices in Linux reside in /dev/ directory. Inspect it with ```ls /dev/``` and make sure you see all 3 newly created block devices there - their names will likely be *xvdb*, *xvdc*, *xvdd*.

![alt text](images/lsblk.png)

5. Use ```df -h``` command to see all mounts and free space on your server

![alt text](<images/df -h.png>)

6. Use gdisk utility to create a single partition on each of the 3 disks.

```sudo gdisk /dev/xvdb```

Follow the below steps :

* Run ```sudo gdisk /dev/xvdb```

* Run a new entry by entering n and click the number of partition in this case 1

* Click yes to complete the process.

![alt text](<images/create partition.png>)

7. Use ```lsblk``` utility to view the newly configured partition on each of the 3 disks.

![alt text](images/2lsblk.png)

8. To install lvm2 package use ```sudo yum install lvm2```.

![alt text](<images/installing lvm2.png>)

* To check for available partitions in the disk, run ```sudo lvmdiskscan``` command

![alt text](<images/lvm disk scan.png>)

9. To mark each of 3 disks as physical volumes (PVs) to be used by LVM, run ```pvcreate``` command for each of the 3 volumes created.

```
sudo pvcreate /dev/xvdb1
sudo pvcreate /dev/xvdc
sudo pvcreate /dev/xvdd

```

![alt text](images/pvcreate.png)

10. To verify that your Physical volume has been created successfully, run ```sudo pvs```

![alt text](<images/sudo pvs.png>)


11. Use ```vgcreate``` utility to add all 3 PVs to a volume group (VG) and name the VG webdata-vg

```sudo vgcreate webdata-vg /dev/xvdb1 /dev/xvdc /dev/xvdd```

![alt text](images/vgcreate.png)

12. To verify that your VG has been created successfully, run ```sudo vgs```

![alt text](<images/sudo vgs.png>)


13. Next we need to create 2 logical volumes using ```lvcreate``` . apps-lv will use half of the PV size while logs-lv Use the remaining space of the PV size. NOTE: apps-lv will be used to store data for the Website while, logs-lv will be used to store data for logs.

```
sudo lvcreate -n apps-lv -L 14G webdata-vg
sudo lvcreate -n logs-lv -L 14G webdata-vg

```

![alt text](<images/sudo lvcreate.png>)

14. To verify that your Logical Volume has been created successfully, run ```sudo lvs``` command

![alt text](<images/sudo lvs.png>)

15. To verify the entire setup, run

```
sudo vgdisplay -v #view complete setup - VG, PV, and LV

sudo lsblk 

```
![alt text](<images/sudo vgdisplay.png>)

![alt text](<images/sudo lsblk.png>)

16. Use ```mkfs.ext4``` to format the logical volumes with ext4 filesystem.

```
sudo mkfs -t ext4 /dev/webdata-vg/apps-lv
sudo mkfs -t ext4 /dev/webdata-vg/logs-lv

```
![alt text](<images/sudo mkfs.png>)


17. Create ```/var/www/html``` directory to store website files

```sudo mkdir -p /var/www/html```

![alt text](images/mkdir.png)

18. Create ```/home/recovery/logs``` to store backup of log data

```sudo mkdir -p /home/recovery/logs```

19. Mount ```/var/www/html``` on apps-lv logical volume

```sudo mount /dev/webdata-vg/apps-lv /var/www/html/```

![alt text](images/mount.png)

20. Use rsync utility to backup all the files in the log directory ```/var/log into /home/recovery/logs``` (This is required before mounting the file system)

```sudo rsync -av /var/log/. /home/recovery/logs/```

![alt text](images/rsync.png)

21. Mount ```/var/log on logs-lv``` logical volume. (Note that all the existing data on /var/log will be deleted. That is why step 19 above is very important).

```sudo mount /dev/webdata-vg/logs-lv /var/log```

![alt text](<images/mount log.png>)

22. Restore log files back into ```/var/log``` directory

```sudo rsync -av /home/recovery/logs /var/log```

![alt text](<images/restore log.png>)

23. 
    Update /etc/fstab file so that the mount configuration will persist after restart of the server.

The UUID of the device will be used to update the ```/etc/fstab``` file;

```sudo blkid```

![alt text](images/blkid.png)

```sudo vi /etc/fstab```

![alt text](images/uuid.png)

Update ```/etc/fstab``` in this format using your own UUID and rememeber to remove the leading and ending quotes.

24. Test the configuration and reload the daemon

```
sudo mount -a
sudo systemctl daemon-reload
```
![alt text](images/systemctl.png)

25. Verify your setup by running ```df -h``` output must look like this:

![alt text](images/verify.png)




