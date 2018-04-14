---
title: Porting Ubuntu Touch
author: tusharm
type: post
date: 2015-08-26T14:16:12+00:00
url: /?p=101
image: /wp-content/uploads/2015/08/ubuntu_touch_foto-655x436.jpg
categories:
  - Project
  - Ubuntu Touch Port
tags:
  - Android
  - CyanogenMod
  - kernel
  - Linux
  - Mobile
  - Port
  - Smartphone
  - Ubuntu

---
As a Minor Project for my College, I have decided upon making a port for Ubuntu Touch to a mobile device. I also have 3 of my friends who will be helping me in completing this project.

We haven&#8217;t yet decided the device we are going to build the ROM for (Moto G3 or the OnePlus One). This is because even though **building it for OnePlus One would be easier**, it already has an 80% functional (some functionalities missing) port of Ubuntu Touch for it.

Also, a previous version of the Guide to porting Ubuntu Touch states that:

> To support a wide range of devices, we decided to use CyanogenMod as a base for the Android system. You could safely use AOSP, as we don&#8217;t use a lot of the customizations and improvements done at the App/Java side, but it&#8217;s easier with CyanogenMod due the scripts and build procedures available for it.

However the current guide says :

> Note that this guide focuses on porting to devices present in the AOSP tree and another version will focus on CyanogenMod based ports.

Whatever the case may be, the drivers and modules for OnePlus will be more readily available (I believe&#8230; and so do a couple of guys on the #ubuntutouch IRC) than those for Moto G3. So, I would prefer to port it to OnePlus One since this will be the first time that I will be trying to do such a project and some reference to previous work done on it would help.

BTW since the device needs to be rooted (Bootloader unlocked to be exact), I think we will be using OnePlus since it is already rooted (in my possession) as opposed to the Moto G3 which is not yet rooted (in my teammates possession).

Currently I am deciding upon a distribution of Linux to work on. I have used Ubuntu, Fedora, Elementary OS, Kali and Red Hat previously but, Since the project itself involves Ubuntu, I am more favoured towards Ubuntu as the system OS too, but using some other Distro would be an adventure as well.

> I would also like to point out here that I have **Previously Built a ROM from the Cyanogen Source** (not changed anything, just compiled the source) during the nightly builds of CM 12.1

**Details of the Project:**

  * **Duration: **4 Months
  * **Members: **4 Members (Me and 3 of my colleagues)

**Requirements:**

  * Linux based System
  * 100GB of Free Space
  * High Speed Internet
  * Enough RAM and Processing power to frequently build the ROM

We will be using the following webpages for reference and help

  * <a href="https://developer.ubuntu.com/en/start/ubuntu-for-devices/porting-new-device/" target="_blank">Ubuntu Touch</a>
  * <a href="http://forum.xda-developers.com/ubuntu-touch/android-ports" target="_blank">XDA Developers</a>
  * <a href="http://wiki.cyanogenmod.org/w/Doc:_porting_intro" target="_blank">CyanogenMod Porting Guide</a>
  * <a href="https://developer.ubuntu.com/en/start/ubuntu-for-devices/installing-ubuntu-for-devices/" target="_blank">Setting up the Environment</a>
  * <a href="http://source.android.com/source/building.html" target="_blank">How to build Android Source</a>
