---
tags:
- Verschlüsselung
- ubuntu
- Resue
- Live-CD
- Linux
- Datensicherung
- snippet
- Rescue
- Knoppix
nid: 1009
permalink: "/blog/2011/07/01/datensicherung-verschluesselte-partition-mit-verschluesseltem-home-verzeichnis-mounten.html"
layout: blog
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

<code>
sudo fdisk -l
</code>

<small>Ausgabe fdisk -l</small>
<code>
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
</code>

Wie oben zu sehen:
<ul>
 <li>/boot liegt auf /dev/sda1 , siehe Bootflag *</li>
 <li>Eine erweiterte Partition auf sda2</li>
 <li>/root auf /dev/sda5</a>
</ul>

<strong>Optional: Tools für die Ver- und Entschlüsselung installieren</strong>

Bei Kubuntu (11.04) CD nicht nötig, 
bei <a href="http://www.knopper.net/">Knoppix</a> (6.4.3 ADRIANE) hingegen schon.

<code>
sudo apt-get update
sudo apt-get install cryptsetup
</code>


<strong>"Öffnen" der verschlüsseten Root-Partition</strong>

<code>
sudo cryptsetup luksOpen /dev/sda5 sda
</code>

Gefolgt von der Eingabe des Passworts.

<code>
Enter passphrase for /dev/sda5:
</code>

.../dev/sda5 ist jetzt auf /dev/mapper/sda5 "gemappt",
ok jetzt "mounten"?!

<strong>Der 1. Versuch /dev/mapper/sda5 zu mounten...</strong>
<strong>mount: unknown filesystem type 'LVM2_member'</strong> 


<code>
sudo mkdir /mnt/sda5
sudo mount /dev/mapper/sda5 /mnt/sda5
</code>


...scheitert an dieser Fehlermeldung:


<code>
mount: unbekannter Dateisystemtyp „LVM2_member“
</code>


<strong>Installation von lvm2, dem Linux Logical Volume Manager</strong>


<code>
sudo apt-get install lvm2
</code>

<strong>Informationen über die Logical Volumes abfragen</strong>


<code>
sudo lvs
</code>



<small>Ausgabe sudo lvs</small>
<code>
  LV     VG      Attr   LSize   Origin Snap%  Move Log Copy%  Convert
  root   box     -wi--- 456.11g
  swap_1 box     -wi---   9.37g
</code>


<strong>Aktivierung der Logical Volumes</strong>


<code>
sudo vgchange -ay  box
</code>



<small>Ausgabe sudo vgchange -ay  box</small>
<code>
  2 logical volume(s) in volume group "box" now active
</code>


<strong>Der 2. Versuch /dev/mapper/sda5 zu mounten...</strong>


<code>
sudo mount /dev/box/root /mnt/sda5
</code>


<strong>Vorbereitung für Chroot-Umgebung</strong>


<code>
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
</code>

<strong>Wechseln in die Chroot-Umgebung</strong>


<code>
sudo chroot $D
</code>

<strong>Benutzer wechseln</strong>


Hier wechseln wir zu dem Benutzer, mit dem wir für gewöhnlich arbeiten.

<code>
su - florian
</code>



<small>Ausgabe su - florian</small>
<code>
keyctl_search: Required key not available
Perhaps try the interactive 'ecryptfs-mount-private'
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.
</code>


(Da wir uns wir uns durch das '-' im obigen Befehl eine "Login-Shell" erhalten ist ein <code>cd</code> und eine Auswertung der "Profile-Dateien nicht mehr nötig.)

<strong>Entschlüsseln des Home-Verzeichnisses</strong>
<code>
ecryptfs-mount-private
</code>



<small>Ausgabe ecryptfs-mount-private nach Eingabe des Passworts</small>
<code>
Enter your login passphrase:
Inserted auth tok with sig [XXXXXXXXXXXXXXXXX] into the user session keyring

INFO: Your private directory has been mounted.
INFO: To see this change in your current shell:
  cd /home/florian
</code>


<strong>Daten auf die externe Festplatte kopieren</strong>


<code>
sudo cp -avr /home/florian /data
</code>

<strong>Quellen</strong>


http://debianforum.de/forum/viewtopic.php?f=29&t=129722#p831828
http://www.cyberciti.biz/faq/ubuntu-mounting-your-encrypted-home-from-livecd/
