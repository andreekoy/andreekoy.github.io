---
layout: post
title:  "Instalasi Centos Web Panel di Centos 7"
date:   2018-08-11
categories: Centos CWP
tags: Centos CWP
comments: true
---

Pada tulisan kali ini saya akan membahas langkah-langkah untuk melakukan Instalasi Centos Web Panel (CWP) di Centos 7.

Untuk CWP sendiri merupakan salah satu panel yang free namun untuk fiturnya tidak kalah dengan panel yang berbayar seperti cPanel ataupun Plesk Panel.

Langkah-langkah yang dilakukan untuk instalasi CWP sendiri sangat mudah, berikut langkah-langkahnya:

•	Siapkan VPS/Cloud server yang masih fresh dan belum terinstall apapun.

•	Jalankan yum upgrade untuk mengupdate VPN/Cloud Server milik anda dengan package yang paling baru. Setelah itu reboot VPS/Cloud server milik anda.

{% highlight bash %}yum –y upgrade{% endhighlight %}

•	Setelah itu set hostname pada VPS/Cloud server milik anda sesuai dengan hostname yang diinginkan.

{% highlight bash %}vi /etc/hostname{% endhighlight %}

•	Jalankan command berikut untuk menginstall CWP

{% highlight bash %}
cd /usr/local/src
wget http://centos-webpanel.com/cwp-latest
sh cwp-latest
{% endhighlight %}

Setelah Instalasi selesai akan muncul informasi URL untuk mengakses Web Panel serta informasi password untuk login. Dan setelah instalasi selesai lanjutkan dengan melakukan reboot.

![cwp Pic](../images/cwp.png)

Dan berikut ini tampilan panel CWP.

![panel Pic](../images/panel.png)
