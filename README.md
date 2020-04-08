# otus_36
# NFS

Домашнее задание
Vagrant стенд для NFS или SAMBA
NFS или SAMBA на выбор:

vagrant up должен поднимать 2 виртуалки: сервер и клиент
на сервер должна быть расшарена директория
на клиента она должна автоматически монтироваться при старте (fstab или autofs)
в шаре должна быть папка upload с правами на запись
- требования для NFS: NFSv3 по UDP, включенный firewall

* Настроить аутентификацию через KERBEROS

____________________________________________________________________________________________________________________________

# Домашняя работа

Статьи, которые помогли:
1) [Установка и настройка NFS сервера / клиента в Centos 7 - идеально, для таких как я, которые видят это в первый раз](https://itdraft.ru/2019/12/09/ustanovka-i-nastrojka-nfs-servera-klienta-v-centos-7/)
2) [Документация из приложенных материалов лекции](https://docs.google.com/document/d/1zFK4AP7O3se-_jQb9N_fPiMrvGIL0SkwpGvPg9EBHRk/edit#)
3) [NFS - Русскоязычная документация](https://help.ubuntu.ru/wiki/nfs)
4) [Как настроить NFS (Network File System) на RHEL/CentOS/Fedora и Debian/Ubuntu](https://andreyex.ru/operacionnaya-sistema-linux/kak-nastroit-nfs-network-file-system-na-rhel-centos-fedora-i-debian-ubuntu/)




```vagrant up``` поднимает 2 vm: server, client

Для проверки:

вход на client
```
vagrant ssh client
```
Каталог, в который будет смонтирована шара, мы создали ранее, теперь монтируем ее:
```
mount -t nfs
```
Посмотреть доступные для монтирования ресурсы хоста ```server``` командой:
```
showmount -e server
```
Запишем файл под пользователем *vagrant*  проверим его наличие: 
```
touch /mnt/nfs-share/upload/file
ls -l /mnt/nfs-share/upload/
```
![Img_alt](https://github.com/Edo1993/otus_36/blob/master/pics/361.png)


Проверяем на стороне ```server``` :

вход на server
```
vagrant ssh server
```
Проверим наличие файла
```
ls -l /mnt/storage/upload/
```
Настройки firewalld:
```
firewall-cmd --state
firewall-cmd --list-all
```
![Img_alt](https://github.com/Edo1993/otus_36/blob/master/pics/362.png)
