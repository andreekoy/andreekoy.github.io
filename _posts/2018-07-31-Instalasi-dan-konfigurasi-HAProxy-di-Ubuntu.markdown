---
layout: post
title:  "Instalasi dan Konfigurasi HAProxy di Ubuntu 16.04"
date:   2018-07-31
categories: Ubuntu LB
comments: true
share: true
---

Pertama-tama Siapkan 3 Buah VM yang akan kita pakai untuk Lab ini, pada topologi ini nantinya salah satu VM ini akan kita install HAProxy dan VM ini akan bertindak sebagai load balancer dan untuk kedua VM lainnya nanti akan bertindak sebagai webserver yang akan menerima request masuk yang sudah di arahkan oleh load balancer.

Berikut masing-masing IP Private dari setiap VM
HA Proxy : 192.168.90.10
web1: 192.168.90.245
web2: 192.168.90.246

**Instalasi HAProxy**

Pertama-tama kita akan melakukan konfigurasi dahulu pada VM HA-Proxynya.

add ppa repository untuk menginstall HAProxy 1.6
{% highlight bash %}sudo add-apt-repository ppa:vbernat/haproxy-1.6{% endhighlight %}

Selanjutnya lakukan update package

{% highlight bash %}sudo apt-get update{% endhighlight %}

Selanjutnya install HAProxy 1.6 denga perintah apt

{% highlight bash %}sudo apt-get install haproxy{% endhighlight %}

Saat ini HAProxy sudah terinstall di mesin anda

**Konfigurasi HAProxy**

Pindah ke direktori konfigurasi HA Proxy

{% highlight bash %}cd /etc/haproxy/{% endhighlight %}

Backup file konfigurasi haproxy untuk berjaga-jaga apabila konfigurasi yang kita lakukan gagal.

{% highlight bash %}cp /etc/haproxy/haproxy.cfg /etc/haproxy/haproxy.cfg.old{% endhighlight %}

Edit file konfigurasi haproxy

{% highlight bash %}nano /etc/haproxy/haproxy.cfg{% endhighlight %}

Pada bagian global tambahkan konfigurasi seperti berikut

{% highlight bash %}
global
log 127.0.0.1 local0 notice
maxconn 2000
user haproxy
group haproxy

Selanjutnya pada bagian default ubah seperti ini
defaults
log global
mode http
option httplog
option dontlognull
retries 3
option redispatch
timeout connect 5000
timeout client 10000
timeout server 10000
{% endhighlight %}

Terakhir kita lakukan konfigurasi pada bagian frontend dan backendnya

{% highlight bash %}
listen appname 0.0.0.0:80
mode http
stats enable
stats uri /haproxy?stats
stats realm Strictly\ Private
stats auth A_Username:YourPassword
stats auth Another_User:passwd
balance roundrobin
option httpclose
option forwardfor
server web1 192.168.90.245:80 check
server web2 192.168.90.246:80 check
{% endhighlight %}

Setelah selesai save lalu restart service HA Proxy dengan command

{% highlight bash %}service haproxy start{% endhighlight %}

Konfigurasi VM Web1 dan Web2

Install apache2 sebagai webserver untuk ke dua VM ini

{% highlight bash %}apt-get install apache2{% endhighlight %}

Setelah itu buat html sederhana untuk mengecek apakah LB kita sudah berjalan

Terakhir tes LB dengan mengakses IP server LB yaitu 192.168.90.10
