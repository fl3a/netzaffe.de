---
tags:
- Verschlüsselung
- ubuntu
- Live-CD
- Linux
- Datensicherung
- snippet
- Rescue
- Knoppix
nid: 1009
layout: post
title: 'Datensicherung: Verschlüsselte Partition mit verschlüsseltem Home-Verzeichnis
  mounten'
created: 1309505066
---
Nach dem Wochenende habe ich bemerkt, daß die Ubuntu-Updates, die ich am Freitag davor durchgeführt habe wohl etwas "verschlimmbessert" haben.

So begrüßt mich am darauffolgenden Montag, direkt eine  <a href="http://twitter.com/#!/fl3a/status/82768200906964992">Kernel-Panic</a>.

Alles im Grunde nichts gravierendes, aber...
<ol>
 <li>Root-Partition ist verschlüsselt</li>
 <li>Home-Verzeichnis ebenfalls verschlüsselt</li>
</ol>
Nunja...

Nach einer Woche <acronym title="Home Office Nerd Deluxe">HOND</acronym> am Laptop und ziemlich zeitintensiver Suche, hier der zusammengetragene, komplette Lösungsweg.
<!--break-->
<strong>Auflistung der Partitionen</strong>

```
sudo fdisk -l
```

```
Disk /dev/sda: 500.1 GB, 500107862016 bytes
255 heads, 63 sectors/track, 60801 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x000d86fc

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *           1          32      248832   83  Linux
/dev/sda2              32       60802   488135681    5  Extended
/dev/sda5              32       60802   488135680   83  Linux
```
<small>Ausgabe fdisk -l</small>

Wie oben zu sehen:
<ul>
 <li>/boot liegt auf /dev/sda1 , siehe Bootflag *</li>
 <li>Eine erweiterte Partition auf sda2</li>
 <li>/root auf /dev/sda5</li>
</ul>

Optional: Tools für die Ver- und Entschlüsselung installieren:
Bei Kubuntu (11.04) CD nicht nötig, bei <a href="http://www.knopper.net/">Knoppix</a> (6.4.3 ADRIANE) hingegen schon.

```
sudo apt-get update
sudo apt-get install cryptsetup
```


"Öffnen" der verschlüsseten Root-Partition

```
sudo cryptsetup luksOpen /dev/sda5 sda
```

Gefolgt von der Eingabe des Passworts.

```
Enter passphrase for /dev/sda5:
```

.../dev/sda5 ist jetzt auf /dev/mapper/sda5 "gemappt", ok jetzt "mounten"?!

Der 1. Versuch /dev/mapper/sda5 zu mounten... `mount: unknown filesystem type 'LVM2_member'` 


```
sudo mkdir /mnt/sda5
sudo mount /dev/mapper/sda5 /mnt/sda5
```


...scheitert an dieser Fehlermeldung:


```
mount: unbekannter Dateisystemtyp „LVM2_member“
```


Installation von lvm2, dem Linux Logical Volume Manager


```
sudo apt-get install lvm2
```

Informationen über die Logical Volumes abfragen


```
sudo lvs
```

```
  LV     VG      Attr   LSize   Origin Snap%  Move Log Copy%  Convert
  root   box     -wi--- 456.11g
  swap_1 box     -wi---   9.37g
```
<small>Ausgabe sudo lvs</small>


Aktivierung der Logical Volumes


```
sudo vgchange -ay  box
```



```
  2 logical volume(s) in volume group "box" now active
```
<small>Ausgabe sudo vgchange -ay  box</small>


Der 2. Versuch /dev/mapper/sda5 zu mounten...


```
sudo mount /dev/box/root /mnt/sda5
```


Vorbereitung für Chroot-Umgebung


```
D=/mnt/sda5
sudo mount -o bind /dev $D/dev
sudo mount -o bind /sys $D/sys
sudo mount -o bind /dev/shm $D/dev/shm
sudo mount -o bind /proc $D/proc
sudo mkdir $D/data
sudo mkdir /mnt/usb_device
sudo mount /dev/sdb1 /mnt/usb_device
sudo mkdir  /dev/sdb1 /mnt/usb_device/bak20110630
sudo mount --rbind  /mnt/usb_device/bak20110630 $D/data/
```

Wechseln in die Chroot-Umgebung


```
sudo chroot $D
```

Benutzer wechseln, hier wechseln wir zu dem Benutzer, mit dem wir für gewöhnlich arbeiten.

```
su - florian
```

```
keyctl_search: Required key not available
Perhaps try the interactive 'ecryptfs-mount-private'
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
```
<small>Ausgabe su - florian</small>


(Da wir uns wir uns durch das '-' im obigen Befehl eine "Login-Shell" erhalten ist ein ```cd``` und eine Auswertung der "Profile-Dateien nicht mehr nötig.)

Entschlüsseln des Home-Verzeichnisses
```
ecryptfs-mount-private
```

```
Enter your login passphrase:
Inserted auth tok with sig [XXXXXXXXXXXXXXXXX] into the user session keyring

INFO: Your private directory has been mounted.
INFO: To see this change in your current shell:
  cd /home/florian
```
<small>Ausgabe ecryptfs-mount-private nach Eingabe des Passworts</small>


Daten auf die externe Festplatte kopieren


```
sudo cp -avr /home/florian /data
```

<strong>Quellen</strong>


- [http://debianforum.de/forum/viewtopic.php?f=29&t=129722#p831828](http://debianforum.de/forum/viewtopic.php?f=29&t=129722#p831828)
- [http://www.cyberciti.biz/faq/ubuntu-mounting-your-encrypted-home-from-livecd/](http://www.cyberciti.biz/faq/ubuntu-mounting-your-encrypted-home-from-livecd/)
