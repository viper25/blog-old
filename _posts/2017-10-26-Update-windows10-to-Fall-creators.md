---
layout: post
title: Update Windows 10 Enterprise to 1709 (Fall Creators Update)
subtitle: Manually update Windows 10 Enterprise
published: true
tags: [technology,windows]
---

So Microsoft released version [1709](https://docs.microsoft.com/en-us/windows/whats-new/whats-new-windows-10-version-1709), also called Fall Creators Update. This post deals with how to upgrade Enterprise editions of Windows to 1709 since Microsoft doesn't push the version 1709 to Enterprise editions. Yet. If you are running the latest version of Windows Enterprise (as of this writing) you should be on version 1703. Verify this checking in *About your PC* 

{: .box-note}
**Note:** This post may be moot or inconsequential at a later date when Microsoft pushes this update to Windows 10 Enterprise editions. It is valid at the time of writing.

![image](https://user-images.githubusercontent.com/32394146/32054698-e3bb957c-ba91-11e7-8bd0-3c48b5d455b7.png)

![image](https://user-images.githubusercontent.com/32394146/32083513-ac941704-baf5-11e7-9fac-0294dcfe6541.png)

If you check for Windows Updates, it doesn't offer an update to 1709. So how do we do it? 

# Upgrade Windows 10 Enterprise

Download the 1709 update from your MSDN Subscriptions. Select the version titled **Windows 10 (multi-edition) VL, Version 1709 (Updated Sept 2017)**. The downloaded ISO is  named *en_windows_10_multi-edition_vl_version_1709_updated_sept_2017_x64_dvd_100090741.iso*
![image](https://user-images.githubusercontent.com/32394146/32055132-79cd40dc-ba93-11e7-8eaf-80b981c9e47d.png)

Mount this in Windows 10 and run setup.
![image](https://user-images.githubusercontent.com/32394146/32055423-5a72ba18-ba94-11e7-959d-656eb9b86966.png)

![image](https://user-images.githubusercontent.com/32394146/32055478-8518d888-ba94-11e7-99f6-ffc692b37e4a.png)

![image](https://user-images.githubusercontent.com/32394146/32055509-9cedd4e0-ba94-11e7-99c6-5d2731d8adac.png)

![image](https://user-images.githubusercontent.com/32394146/32055784-59b18e46-ba95-11e7-9b66-aa2d3ce8bab5.png)

After about 20 mins or so of installation and a few restarts, we're now on 1709! 

![image](https://user-images.githubusercontent.com/32394146/32060282-e1f21e8c-baa0-11e7-85a4-8e818f12672f.png)

The one feature I wanted was the *[OneDrive Files On-Demand](https://support.office.com/en-us/article/Learn-about-OneDrive-Files-On-Demand-0e6860d3-d9f3-4971-b321-7092438fb38e?ui=en-US&rs=en-US&ad=US)* feature. This is enabled ONLY if you are on Windows version 1709 - which I now am!

![image](https://user-images.githubusercontent.com/32394146/32060322-ff34bb6c-baa0-11e7-9afb-b608655c6d8d.png)

The folder here is 627MB but only occupies 28KB on disk 
![image](https://user-images.githubusercontent.com/32394146/32259105-8a92e7a6-bf01-11e7-9da0-6fffab58aec8.png)


# Cleanup installation files

As expected, the rest of my applications, folders, settings are all intact. The upgrade does create a ~23 GB folder `Windows.old` folder in your C:\ drive

![image](https://user-images.githubusercontent.com/32394146/32060695-28590cb8-baa2-11e7-8413-0cc3151ca282.png)

But you can remove that using *Disk Cleanup* and select the option as shown below:

![image](https://user-images.githubusercontent.com/32394146/32061029-1d3c6eaa-baa3-11e7-951e-f97c82aff9c5.png)
