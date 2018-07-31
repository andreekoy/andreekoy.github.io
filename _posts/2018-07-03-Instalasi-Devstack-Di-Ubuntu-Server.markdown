---
layout: post
title:  "Instalasi Devstack di Ubuntu Server 16.04"
date:   2018-07-31
categories: Openstack Ubuntu
tags: Openstack Ubuntu
comments: true
---

Pada tulisan kali ini saya akan menjelaskan instalasi Openstack menggunakan Devstack. Untuk deployment ini saya menggunakan Distro Ubuntu 16.04. Untuk deployment openstack sendiri selain menggunakan devstack di Ubuntu dapat juga menggunakan conjure-up mungkin akan saya bahas di lain waktu. 

Kali ini kita akan membangun Openstack pada Singe Machine, untuk spesifikasi yang kali ini saya pakai, saya setting menggunakan 4x4 CPU, 16GB RAM dan HDD 80GB. Untuk minimal spesifikasinya sendiri dapat menggunakan 8CPU dan 12 GB Ram. 
Berikut langkah-langkah untuk melakukan instalasi Devstack di Ubuntu 16.04.

•	Siapkan sebuah Server/VM yang sudah diinstall Ubuntu 16.04. Saat instalasinya saya menyarankan untuk menggunakan guided LVM partition. Dan LVM ini diperlulan oleh service Cinder untuk membuat volume.

•	Selanjutnya setelah itu install python systemd, python system ini diperlukan oleh devstack untuk memanage service dan library yang diperlukan untuk diinstall. Jalankan command berikut untuk melakukan instalasi python systemd.

{% highlight bash %}[andreas@devstack ~]$ sudo apt-get install -y python-systemd{% endhighlight %}

Service yang akan diinstall dan dijalankan oleh Devstack memerlukan user account, untuk itu kita akan membuat user yang memiliki akses ke sudo, Jalankan command berikut untuk membuat user.

{% highlight bash %}[andreas@devstack ~]$ sudo useradd -s /bin/bash -d /opt/stack -m stack
[andreas@devstack ~]$ echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack{% endhighlight %}

Selanjutnya untuk instalasi Devstack kita perlu melakukan cloning GIT repo, jalankan command berikut untuk melakukan cloning GIT repo Devstack.

{% highlight bash %}[andreas@devstack ~]$ sudo su -l stack
[andreas@devstack ~]$ git clone https://git.openstack.org/openstack-dev/devstack
[andreas@devstack ~]$ cd /opt/stack/devstack{% endhighlight %}

Selanjutnya buat Devstack answer file, pada direktori devstack buat file bernama local.conf. Pada file tersebut kita akan diisi dengan password service-service dan admin Devstack.

{% highlight bash %}[stack@devstack ~]$ sudo nano local.conf{% endhighlight %}

{% highlight bash %}
[[local|localrc]]
ADMIN_PASSWORD=Password1
DATABASE_PASSWORD=$ADMIN_PASSWORD
RABBIT_PASSWORD=$ADMIN_PASSWORD
SERVICE_PASSWORD=$ADMIN_PASSWORD
HOST_IP=IP_Address_Server
{% endhighlight %}

Selanjutnya edit file /etc/hosts dan masukkan IP address beserta hostname server.
{% highlight bash %}[stack@devstack ~]$ sudo nano /etc/hosts{% endhighlight %}

{% highlight bash %}
10.0.2.4  devstack
{% endhighlight %}

Selanjutnya jalankan script instalasi pada direktori devstack. Jalankan scrip stack.sh untuk memulai instalasi Devstack.

{% highlight bash %}[stack@devstack ~]$ ./stack.sh{% endhighlight %}

Setelah itu tunggu hingga Instalasi Selesai, untuk waktunya bervariasi tergantung koneksi dan spesifikasi yang digunakan. 

Setelah selesai akan muncul informasi URL dashboard horizon serta credential admin user dan password Openstack.

![Devstask Pic](../images/devstack.png)


