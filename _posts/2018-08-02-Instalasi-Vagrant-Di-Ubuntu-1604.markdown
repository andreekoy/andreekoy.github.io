---
layout: post
title:  "Instalasi Vagrant di Ubuntu 16.04"
date:   2018-08-1
categories: Ubuntu Vagrant
comments: true
share: true
---
Pada kali ini saya akan menjelaskan tentang instalasi vagrant di Ubuntu 16.04. Vagrant sendiri adalah....


Pertama-tama update dahulu repositori pada VM milik anda.
{% highlight bash %}apt-get update{% endhighlight %}

Setelah meng-update repo, selanjutnya install virtualbox dan vagrant dengan command berikut:
{% highlight bash %}apt-get install virtualbox vagrant{% endhighlight %}

Setelah vagrant terinstall, verifikasi apakah vagrant sudah terinstall dengan command vagrant:
{% highlight bash %}vagrant{% endhighlight %}

{% highlight bash %}
Usage: vagrant [options] <command> [<args>]

    -v, --version                    Print the version and exit.
    -h, --help                       Print this help.

Common commands:
     box             manages boxes: installation, removal, etc.
     destroy         stops and deletes all traces of the vagrant machine
     global-status   outputs status Vagrant environments for this user
     halt            stops the vagrant machine
     help            shows the help for a subcommand
     init            initializes a new Vagrant environment by creating a Vagrantfile
     login           log in to HashiCorp's Vagrant Cloud
     package         packages a running vagrant environment into a box
     plugin          manages plugins: install, uninstall, update, etc.
     port            displays information about guest port mappings
     powershell      connects to machine via powershell remoting
     provision       provisions the vagrant machine
     push            deploys code in this environment to a configured destination
     rdp             connects to machine via RDP
     reload          restarts vagrant machine, loads new Vagrantfile configuration
     resume          resume a suspended vagrant machine
     snapshot        manages snapshots: saving, restoring, etc.
     ssh             connects to machine via SSH
     ssh-config      outputs OpenSSH valid configuration to connect to the machine
     status          outputs status of the vagrant machine
     suspend         suspends the machine
     up              starts and provisions the vagrant environment
     version         prints current and latest Vagrant version

For help on any individual command run `vagrant COMMAND -h`

Additional subcommands are available, but are either more advanced
or not commonly used. To see all subcommands, run the command
`vagrant list-commands`.
{% endhighlight %}



