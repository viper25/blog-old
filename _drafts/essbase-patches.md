---
layout: post
title: Apply patches to Essbase
subtitle: Apply patches to an Essbase instance on Windows
published: true
tags: Essbase
---

Installing Essbase is a two stage process. The first is the **Installation of Essbase bits** and the second is the **Configuration** of Essbase. Once installed, Essbase can be reconfigured multiple times (say when the back end database server changes). If you need to add additional Essbase components, you'd need to re-run the Installation process. These details are present in Oracle documentation but one has to hunt it down. Essbase requires a backend database for it's operation (to store Essbase meta data). This post assumes you have a SQL Server database ready to connect to.

# Downloading the Essbase bits

Create an account in [http://edelivery.oracle.com](http://edelivery.oracle.com) and download the bits.

![image](https://user-images.githubusercontent.com/32394146/31257109-4f86ddd6-aa69-11e7-9f00-9178588335a7.png)

Select Microsoft x64 as the platform


