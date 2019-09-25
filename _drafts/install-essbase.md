---
layout: post
title: Install Essbase on Windows
subtitle: Essbase 11.1.2.4 on Windows 2012
published: true
tags: Essbase
---

Installing Essbase is a two stage process. The first is the **Installation of Essbase bits** and the second is the **Configuration** of Essbase. Once installed, Essbase can be reconfigured multiple times (say when the back end database server changes). If you need to add additional Essbase components, you'd need to re-run the Installation process. These details are present in Oracle documentation but one has to hunt it down. Essbase requires a backend database for it's operation (to store Essbase meta data). This post assumes you have a SQL Server database ready to connect to.

# Downloading the Essbase bits

Create an account in [http://edelivery.oracle.com](http://edelivery.oracle.com) and download the bits.

![image](https://user-images.githubusercontent.com/32394146/31257109-4f86ddd6-aa69-11e7-9f00-9178588335a7.png)

Select Microsoft x64 as the patform

{: .box-error}
**Error:** This selection doesn't seem to work on Chrome; Use IE or Edge.


![image](https://user-images.githubusercontent.com/32394146/31257157-89335f96-aa69-11e7-8368-048d646c6aba.png)

Once downloaded, unzip all the zip files to a single folder, say `C:\download\` & overwrite when asked to.

# Installing Essbase

Before installing, [disable UAC](https://www.howtogeek.com/howto/windows-vista/disable-user-account-control-uac-the-easy-way-on-windows-vista/). 

![image](https://user-images.githubusercontent.com/32394146/31227699-67c58958-aa0d-11e7-9d28-9378da4752e9.png)


![image](https://user-images.githubusercontent.com/32394146/31227715-74da10d2-aa0d-11e7-89e5-d42f0aec3b4c.png)

![image](https://user-images.githubusercontent.com/32394146/31227726-7f78934c-aa0d-11e7-9b71-0cde1f5ebc28.png)

![image](https://user-images.githubusercontent.com/32394146/31227924-2b2d22d4-aa0e-11e7-91ff-17cdb70e0cde.png)


If you want to install Essbase in standalone mode (not using Foundation Services), you can skip the installation for Foundation Services Web applications. However, you must configure the Shared Services Registry database. 

# Configuring Essbase

Essbase is now installed. We need to configure Essbase using EPM System COnfigurator.

![image](https://user-images.githubusercontent.com/32394146/31228003-8634ceb6-aa0e-11e7-8b30-a934305e0994.png)

![image](https://user-images.githubusercontent.com/32394146/31228022-968f338c-aa0e-11e7-8ba3-b1dd2ab19b33.png)

![image](https://user-images.githubusercontent.com/32394146/31228109-dde010f8-aa0e-11e7-9829-f9745c1d6739.png)

If you are re-using an existing table (say when you are re-configuring an existing Essbase instance), you'll get the message below:

![image](https://user-images.githubusercontent.com/32394146/31233130-766a8164-aa1e-11e7-9be4-d98b96e360f2.png)

If you are re-configuring, DO NOT drop existing tables. If you do not care for the any existing Essbase instances that are configured, click Yes and drop the tables - you will have a brand new Essbase instance configured.

![image](https://user-images.githubusercontent.com/32394146/31233139-7fbf23a0-aa1e-11e7-9ed9-b8cee753c5b9.png)

![image](https://user-images.githubusercontent.com/32394146/31233152-85fea27c-aa1e-11e7-8215-dc4e06843d92.png)

![image](https://user-images.githubusercontent.com/32394146/31233586-93f5b504-aa1f-11e7-9a5e-60fb76be5b59.png)

If you are configuring first time to the Database select Perform first-time configuration of Database  and if it’s the second time you can select Connect to a previosuly configured Database.

![image](https://user-images.githubusercontent.com/32394146/31233608-a2a4d83c-aa1f-11e7-808b-2d388e08c86c.png)

![image](https://user-images.githubusercontent.com/32394146/31233669-bc2ff6ec-aa1f-11e7-9a38-fa215b397159.png)

![image](https://user-images.githubusercontent.com/32394146/31236172-fb07993c-aa25-11e7-86b3-37e250faca33.png)

In Binding Host name: provide the Load Balancer or Cluster name of the Essbase installation.

![image](https://user-images.githubusercontent.com/32394146/31236218-1f3592fa-aa26-11e7-8585-6c00693377f9.png)

![image](https://user-images.githubusercontent.com/32394146/31236320-5b66e29c-aa26-11e7-8a11-f820526b6b4e.png)

![image](https://user-images.githubusercontent.com/32394146/31236332-62687146-aa26-11e7-9ea5-97786e8b380b.png)

### Optional Performance configuration

In `$ARBORPATH/bin/essbase.cfg` i.e for example at `F:\Oracle\Middleware\user_projects\epmsystem1\EssbaseServer\essbaseserver1\bin` add the following lines to enable large calcs to take place:

```
CalcLockBlockHigh 2000
CalcLockBlockDefault 200
CalcLockBlocklow 50
```

If not, you’ll see errors in the logs such as :

<span style="color:red">
Dynamic Calc processor cannot lock more than [100] ESM blocks during the calculation, please increase CalcLockBlock setting and then retry(a small data cache setting could also cause this problem, please check the data cache size setting).
</span>

### Speed up restructures

Set the following to speed up restructures:

```
RESTRUCTURETHREADS 12
```

In a server that has 2 CPU with 6 cores each, you can set a max of 12 threads. You can find this by running on a DOS window:

```
WMIC CPU Get DeviceID,NumberOfCores,NumberOfLogicalProcessors
```

![image](https://user-images.githubusercontent.com/32394146/31236869-e61513c2-aa27-11e7-9682-8aab7fc673ff.png)

For example, set to 12, on doing a restructure it uses 12 threads and restructures in parallel as can be seen below:

![image](https://user-images.githubusercontent.com/32394146/31236947-1c3db256-aa28-11e7-8866-4dd8b9c59828.png)

### Configuring Java Heap size 

In `E:\Oracle\Middleware\user_projects\epmsystem1\bin\deploymentScripts` edit `setCustomParamsEPMServer.bat` to edit the following (highlighted):

```
set USER_MEM_ARGS=-Xms3072m -XX:PermSize=64m -XX:MaxPermSize=512m -Xmx8000m
```
