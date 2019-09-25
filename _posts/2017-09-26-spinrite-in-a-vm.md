---
layout: post
title: Run SpinRite from a Virtual Machine (VM)
subtitle: How to run SpinRite in a VM testing multiple disks at once
published: true
tags: technology
---


[SpinRite](https://www.grc.com/sr/spinrite.htm) is used to work on failed/failing hard disks, SSDs. The problem with SpinRite is that the current version (6.0) was released more than a decade ago in 2004. As such, not all computers may be boot into SpinRite and detect hard disks. It doesn't support UEFI hence, one solution is to see if we can run SpinRite in a VM and then access raw disks to scan. Here's how we do it:

{: .box-warning}
**Warning**: This is a semi-advanced topic, since we deal with raw disk (not managed by the OS); any mistakes might render the disk unreadable. Proceed at your own risk.

## Pepare the SpinRite VM
You need a Virtual Machine on which to run SpinRite. First order of business is to install [Oracle VirtualBox](http://www.oracle.com/technetwork/server-storage/virtualbox/downloads/index.html). Pretty simple, it's just clicking Next > Next > Next.

Generate the SpinRite ISO (per SpinRite's instructions). Now create a VM in Oracle VirtualBox:

![image](https://user-images.githubusercontent.com/327990/30996149-0a49d2e6-a4f1-11e7-92c8-8d6d3636b960.png)

Even 64MB for the VM is enough

![image](https://user-images.githubusercontent.com/327990/30996153-1b9bb2ee-a4f1-11e7-95a4-df1aab122ad7.png)

![image](https://user-images.githubusercontent.com/327990/30996159-2c955384-a4f1-11e7-99cf-e8f87b14335d.png)

![image](https://user-images.githubusercontent.com/327990/30996164-3f87bb08-a4f1-11e7-8f18-f8bf4d5a8014.png)

Point to the SpinRite ISO.

![virtualbox_2017-09-29_13-00-04](https://user-images.githubusercontent.com/327990/31001459-6584f594-a516-11e7-8232-2e59f70fc278.png)

## Identify and Detach disk

Attach the disk (you with to scan) to your machine and open Disk Management. Identify your Disk #.

![image](https://user-images.githubusercontent.com/327990/30996101-b56ab358-a4f0-11e7-8eaa-05049466a4b1.png)

In the example above, it's 2. Note this. Now, we need to detach the disk from Windows. Run an elevated command prompt (as Administrator), then run `diskpart`.  You'll enter the diskpart shell and then issue these commands. 

~~~
list disk
select disk #
offline disk
attribute disk clear readonly
rescan
~~~

![image](https://user-images.githubusercontent.com/327990/30956072-83a52ebc-a468-11e7-9aaf-349c00750189.png)


The disk is now offline

![image](https://user-images.githubusercontent.com/327990/30954680-a3add042-a463-11e7-8e6c-48d9f4207b8a.png)

  
## Create the Disk Image

Create a Disk Image from whole drive. Goto the install directory of VirtualBox. For me it's `D:\Program Files\Oracle\VirtualBox`. Open this path in a command prompt (as an Administrator). Replace the number (in the command below) with the Disk Number as appears in the DISKPART command or as seen in Computer Management (msc) > Disk Management

~~~
VBoxManage internalcommands createrawvmdk -filename "T:\Disk2.vmdk" -rawdisk "\\.\PhysicalDrive2"
~~~

i.e. if your Disk number is 3, `PhysicalDrive2` should be `PhysicalDrive3`. The `-filename` can be any name you choose.

Now launch VirtualBox (as Administrator again, else you won't be able to attach the Virtual Disk) and create a SpinRite VM

![image](https://user-images.githubusercontent.com/327990/30996112-cb63378e-a4f0-11e7-8824-c178922ba484.png)

{: .box-note}
**Tip:** You can create multiple VMs if you wish to scan multiple disks at one time


![image](https://user-images.githubusercontent.com/327990/30996176-4e418520-a4f1-11e7-8bc8-223bfabd07fc.png)

Attach the disk we created before

![image](https://user-images.githubusercontent.com/327990/30996184-5e3217d8-a4f1-11e7-8627-25d0e6a7ab0a.png)

This disk will appear attached to the VM

![image](https://user-images.githubusercontent.com/327990/30996188-6d83099a-a4f1-11e7-8e18-aaea51cac873.png)

Now just start the VM and you will be able to boot into SpinRite. You can see the 500GB disk has been recognized via the VM.

![image](https://user-images.githubusercontent.com/327990/30955781-6fe1465a-a467-11e7-8e87-af34443b8540.png)


{: .box-note}
**With helpful notes from [Dan Fox](https://romaimperator.com/?p=29)**

Scan away!
