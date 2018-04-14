---
title: The Linux Mint Adventure
author: tusharm
type: post
date: 2015-08-28T09:26:38+00:00
url: /?p=20
image: /wp-content/uploads/2015/08/mintlogo-color-1.jpg
categories:
  - Project
  - Ubuntu Touch Port

---
So I finally decided to go with Linux Mint for the platform on which I would build the Ubuntu Touch Port. This is only a temporary decision though since I can change it to Ubuntu or anything else if it doesn&#8217;t fulfill my needs.

**Why Linux Mint? **Because it recently I installed Windows 10 (relatively new right now) on my system and it has a great UI. So I was looking for a distribution that would be able to compete with that. Also I had never tried Linux Mint out before.

Installation was pretty straight forward. I downloaded the 64 bit Cinnamon based ISO and flashed it onto a 500GB hardrive (had no free pendrive at the time) using YUMI multiboot installer. The USB 3.0 connection helped installing it faster. Then I added the OS as the 2nd OS overwriting the previous Ubuntu Installation.

> Linux Mint didn&#8217;t ask me if I wanted to Install the OS until it had already booted into the Live OS. This however was not the case with Ubuntu or Fedora or Kali even. I may have missed something but that was a teeny bit annoying.

&nbsp;

**My Experience with Linux Mint**

**Blazing Fast:** Maybe this is because I came from a clogged up Ubuntu Environment to a Windows one and then to a new installation of a widely  used OS. But I was taken aback by the speed this OS has. Applications open up instantly and I couldn&#8217;t notice any lag till now (almost 15 hrs since installation). However I did have to shut down the laptop once since I started writing this post. This happened when I was transferring an ISO file of Windows to my friend&#8217;s pendrive and the OS just went slow.. very slow. A reboot fixed it though.

&nbsp;

**Better UI: **Comparing this to Ubuntu, it is really a very good upgrade. The controls are not intrusive yet readily available when required. It is also more pleasing to the eye than the rounded edges of Ubuntu. Now I know that Ubuntu and Linux Mint both can be themed to look exactly as you want but this post is about the Out of the Box Experience which was pretty good.

**<img class="aligncenter size-full wp-image-22" src="https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2015/08/Screenshot-from-2015-08-28-054300.png?resize=1040%2C585" alt="Linux Mint Networks Screenshot" srcset="https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2015/08/Screenshot-from-2015-08-28-054300.png?w=1366 1366w, https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2015/08/Screenshot-from-2015-08-28-054300.png?resize=300%2C169 300w, https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2015/08/Screenshot-from-2015-08-28-054300.png?resize=768%2C432 768w, https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2015/08/Screenshot-from-2015-08-28-054300.png?resize=1024%2C576 1024w, https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2015/08/Screenshot-from-2015-08-28-054300.png?resize=1200%2C675 1200w" sizes="(max-width: 1040px) 100vw, 1040px" data-recalc-dims="1" />Wifi Driver: **My laptop was not very widely bought when it was released and so, it was no surprise that I had to install **bcmwl-kernel-source **using my mobile&#8217;s tethered connection to be able to connect to my college&#8217;s wifi. A pretty straightforward procedure that I have done many times. Also, I had to install CNTLM to be able to use the College&#8217;s wifi since it uses NTLM Authentication which is not natively supported by Linux.

[<img class="aligncenter size-full wp-image-23" src="https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2015/08/Screenshot-from-2015-08-28-055319.png?resize=1040%2C585" alt="CNTLM Linux Mint Install" srcset="https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2015/08/Screenshot-from-2015-08-28-055319.png?w=1366 1366w, https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2015/08/Screenshot-from-2015-08-28-055319.png?resize=300%2C169 300w, https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2015/08/Screenshot-from-2015-08-28-055319.png?resize=768%2C432 768w, https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2015/08/Screenshot-from-2015-08-28-055319.png?resize=1024%2C576 1024w, https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2015/08/Screenshot-from-2015-08-28-055319.png?resize=1200%2C675 1200w" sizes="(max-width: 1040px) 100vw, 1040px" data-recalc-dims="1" />][1]

**Terminal Proxy Configuration: **Once I installed CNTLM, I set up the OS to apply a system wide proxy directed at http://127.0.0.1:3128 which is the default proxy used by it. This hoewever does not apply the proxy to the terminal of the OS (similar to Ubuntu). So, I exported the proxy to the terminal using

> $ export http_proxy=http://127.0.0.1:3128

This normally worked with Ubuntu but with Linux Mint it didn&#8217;t. After some googling I found out that I could run command on the terminal if I used sudo -E which sets the command after it to forcefully use the User Environment variables.

To overcome this issue , I had to run

> $ sudo visudo

and then add the following line to the file:

> Defaults env\_keep += &#8220;ftp\_proxy http\_proxy https\_proxy no_proxy&#8221;

<pre></pre>

**Final Words**

Linux Mint is a great OS not just for beginners but for anyone that is looking for a good UI that doesn&#8217;t interrupt your work and complements it instead. I believe that it will be appreciated by anyone who has a taste for good UI and great support.

> I **do not** regret the decision to use this as the daily OS.

 [1]: https://i2.wp.com/blog.tusharmishra.in/wp-content/uploads/2015/08/Screenshot-from-2015-08-28-055319.png
