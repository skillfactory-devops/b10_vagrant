## B10.5 Используем Vagrant для запуска старого кода

* Добавил в источники пакетов /etc/apt/sources.list.d репозиторий Virtualbox, добавил PGP-ключ для проверки подписи репозитория,
* Установил headless-вариант VirtualBox с помощью `apt-get install virtualbox-7.1` по [мануалу](https://www.virtualbox.org/manual/topics/installation.html),
* Разрешил своему пользователю использовать VirtualBox с помощью `usermod -a -G vboxusers user`,
* Добавил в источники пакетов Vagrant,
* Установил с помощью `apt install vagrant`,
* Проверил работоспособность по [мануалу Getting Started](https://developer.hashicorp.com/vagrant/tutorials/getting-started),
* Нашёл нужный Vagrant Box [поисковым запросом](https://portal.cloud.hashicorp.com/vagrant/discover?query=postgresql%208.4),
* Создал Box:
```
$ mkdir pg8.4
$ cd pg8.4
$ vagrant init irbisnet/postgresql-8.4 --box-version 1.0.0
```
* Отредактировал [Vagrantfile](https://github.com/skillfactory-devops/b10_vagrant/blob/main/Vagrantfile), запустил Box:
```
$ vagrant up
Bringing machine 'default' up with 'virtualbox' provider...
==> default: Box 'irbisnet/postgresql-8.4' could not be found. Attempting to find and install...
    default: Box Provider: virtualbox
    default: Box Version: 1.0.0
==> default: Loading metadata for box 'irbisnet/postgresql-8.4'
    default: URL: https://vagrantcloud.com/api/v2/vagrant/irbisnet/postgresql-8.4
==> default: Adding box 'irbisnet/postgresql-8.4' (v1.0.0) for provider: virtualbox
    default: Downloading: https://vagrantcloud.com/irbisnet/boxes/postgresql-8.4/versions/1.0.0/providers/virtualbox/unknown/vagrant.box
==> default: Successfully added box 'irbisnet/postgresql-8.4' (v1.0.0) for 'virtualbox'!
==> default: Importing base box 'irbisnet/postgresql-8.4'...
==> default: Matching MAC address for NAT networking...
==> default: Checking if box 'irbisnet/postgresql-8.4' version '1.0.0' is up to date...
==> default: Setting the name of the VM: pg84_default_1733503373561_71053
==> default: Fixed port collision for 22 => 2222. Now on port 2200.
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
==> default: Forwarding ports...
    default: 22 (guest) => 2200 (host) (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2200
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: Warning: Connection reset. Retrying...
    default: Warning: Connection reset. Retrying...
==> default: Machine booted and ready!
==> default: Checking for guest additions in VM...
    default: The guest additions on this VM do not match the installed version of
    default: VirtualBox! In most cases this is fine, but in rare cases it can
    default: prevent things such as shared folders from working properly. If you see
    default: shared folder errors, please make sure the guest additions within the
    default: virtual machine match the version of VirtualBox you have installed on
    default: your host and reload your VM.
    default: 
    default: Guest Additions Version: 4.3.40
    default: VirtualBox Version: 7.1
==> default: Mounting shared folders...
    default: /home/al/pg8.4 => /vagrant
al@debian:~/pg8.4$ vagrant ssh
Welcome to Ubuntu 14.04.6 LTS (GNU/Linux 3.13.0-170-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

 System information disabled due to load higher than 1.0

New release '16.04.7 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


Last login: Mon Sep 13 17:37:14 2021 from 10.0.2.2
vagrant@vagrant-ubuntu-trusty-64:~$ pg_isready 
/var/run/postgresql:5432 - no response
$ exit
logout
```
