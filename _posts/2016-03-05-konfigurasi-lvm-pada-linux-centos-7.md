---
id: 170
title: Membuat Konfigurasi LVM pada Linux (CentOS 7)
date: 2016-03-05T23:24:31+00:00
author: Eko Junaidi Salam
layout: post
guid: http://ekojunaidisalam.com/?p=170
permalink: /2016/03/05/konfigurasi-lvm-pada-linux-centos-7/
dsq_thread_id:
  - "4636722675"
dsq_needs_sync:
  - "1"
categories:
  - Artikel
  - Linux
  - Teknologi
  - 'Tip &amp; Trik'
tags:
  - Centos 7
  - Linux
  - LVM
  - lvm2
  - lvmdiskscan
  - rsync
---
<h2 style="text-align: center;">
  <a href="https://ekojunaidisalam.com/wp-content/uploads/2016/03/LVM.png" rel="attachment wp-att-171"><img class="aligncenter wp-image-171 size-large" src="https://ekojunaidisalam.com/wp-content/uploads/2016/03/LVM-1024x944.png" alt="Konfigurasi LVM" width="584" height="538" srcset="https://ekojunaidisalam.com/wp-content/uploads/2016/03/LVM-1024x944.png 1024w, https://ekojunaidisalam.com/wp-content/uploads/2016/03/LVM-300x277.png 300w, https://ekojunaidisalam.com/wp-content/uploads/2016/03/LVM-768x708.png 768w, https://ekojunaidisalam.com/wp-content/uploads/2016/03/LVM-325x300.png 325w, https://ekojunaidisalam.com/wp-content/uploads/2016/03/LVM.png 1165w" sizes="(max-width: 584px) 100vw, 584px" /></a>Konfigurasi LVM pada Linux (Centos 7)
</h2>

<p style="text-align: justify;">
  LVM adalah singkatan dari <em>Logical Volume Management</em> yang digunakan sebagai <em>Device Mapper</em> pada <em>Linux Kernel</em>. Singkatnya LVM ini adalah alat yang digunakan untuk me-<em>mapping</em> harddisk kita di lingkungan OS Linux sehingga dari beberapa harddisk bisa di gabung menjadi 1 disk besar yang mudah untuk di <em>extend</em> atau di <em>resize </em>baca <em><strong>(E-R)</strong></em>, disini saya khususkan untuk Konfigurasi LVM pada Centos 7.
</p>

<p style="text-align: justify;">
  Mengapa harus LVM ?, dengan <em><strong>GParted</strong> </em>atau <em><strong>Partition Magic</strong></em> aja sudah cukup untuk (e-r) partisi. Ya anda benar, bila itu hanya untuk (e-r) partisi dalam 1 harddisk. Bila anda memiliki 1 partisi dalam 1 harddisk <em><strong>Non-RAID</strong></em> berukuran 500GB, dan anda butuh untuk (e-r) partisi tersebut menjadi 800GB dengan konfigurasi 1 harddisk tambahan <em><strong>Non-RAID</strong></em>, LVM bisa melakukan itu untuk anda. Tanpa <strong>LVM</strong> apalagi <strong>Non-RAID</strong> anda tak bisa melakukannya.<a name='more'></a>
</p>

<p style="text-align: justify;">
  Gambar diatas sudah cukup menjelaskan struktur dari LVM, bagaimana dia menggabungkan banyak hdd menjadi 1 Volume Group besar sehingga nantinya dapat dipecah-pecah kembali bila diperlukan. Jadi, bagaimana membuat LVM ?, Ikutilah petunjuk dibawah ini, segala hal yang berakibat <span style="color: #ff0000;"><strong>FATAL</strong> </span>setelah melakukan petunjuk ini <span style="color: #ff0000;"><strong>diluar tanggung jawab penulis</strong></span>, segala resiko ditanggung anda sendiri lakukan full backup sistem sebagai antisipasi atau lakukan menggunakan lingkungan virtual seperti <a href="https://www.virtualbox.org/wiki/Downloads" target="_blank"><strong>VirtualBox</strong></a>.
</p>

<p style="text-align: justify;">
  Desain Sistem Server :
</p>

<p style="text-align: justify;">
  1 HDD 8GB Non-RAID Non-LVM<br /> SDA<br /> |__ sda1 &#8211;> /boot #Boot Partition dg File sistem Ext4<br /> |__ sda2 &#8211;> / #Root Partition dg File sistem Ext4<br /> |__ sda3 &#8211;> /swap #Linux SWAP
</p>

<p style="text-align: justify;">
  Dengan tambahan 2 HDD @ 8 GB nantinya, dengan maksud agar dapat digabung menjadi 16GB dalam 1 partisi data yakni &#8220;/home&#8221;. Tools yang diperlukan :
</p>

<li style="text-align: justify;">
  Install putty
</li>
<li style="text-align: justify;">
  Install lvm2 &#8211;> yum install lvm2 -y
</li>
<li style="text-align: justify;">
  Install rsync &#8211;> yum install rsync -y
</li>
<li style="text-align: justify;">
  Ready to LVM&#8230;
</li>

<p style="text-align: center;">
  <a href="https://ekojunaidisalam.com/wp-content/uploads/2016/03/Desain-awal-sistem.png" rel="attachment wp-att-175"><img class="aligncenter wp-image-175 size-full" src="https://ekojunaidisalam.com/wp-content/uploads/2016/03/Desain-awal-sistem.png" alt="Desain awal sistem" width="675" height="424" srcset="https://ekojunaidisalam.com/wp-content/uploads/2016/03/Desain-awal-sistem.png 675w, https://ekojunaidisalam.com/wp-content/uploads/2016/03/Desain-awal-sistem-300x188.png 300w, https://ekojunaidisalam.com/wp-content/uploads/2016/03/Desain-awal-sistem-478x300.png 478w" sizes="(max-width: 675px) 100vw, 675px" /></a>Tampilan disk awal pada Instalasi Centos 7 Minimal
</p>

<p style="text-align: justify;">
  Sekarang tambahkan 2 HDD @ 8GB pada sistem anda. Kemudian ikuti perintah berikut secara berurutan.
</p>

<p style="text-align: justify;">
  1. Cek disk yang baru ditambahkan. Bila ada sdb dan sdc itu berarti hdd baru anda telah terbaca.<br /> <code>ls /dev/sd*</code><br /> 2. Buat partisi pada disk baru tersebut berurutan dari sdb &#8211; sdc<br /> <code>fdisk /dev/sdb</code><br /> 3. Pada kotak dialog pertama fdisk tekan <code>n [enter], p [enter], 1 [enter] [enter] [enter], t [enter], 8e [enter], w [enter]</code><br /> 4. Lalu cek kembali partisi menggunakan fdisk<br /> <code>fdisk -l /dev/sd*</code><br /> 5. Pastikan LVM Physical Volume 0, Volume Group tidak ada dan /home tidak ada.<br /> <code>lvmdiskscan && vgscan && df -h</code><br /> 6. Buatlah LVM Physical Volume pada partisi /dev/sdb1 dan /dev/sdc1<br /> <code>pvcreate /dev/sdb1 /dev/sdc1</code><br /> 7. Cek kembali LVM Physical Volume, pastikan disitu terdapat 2 LVM Physical Volume<br /> <code>lvmdiskscan</code><br /> 8. Buatlah Volume group dari 2 partisi tersebut, dengan nama group &#8220;ejs&#8221; tanpa quotes.<br /> <code>vgcreate ejs /dev/sdb1 /dev/sdc1</code><br /> 9. Cek hasilnya dengan melihat LVM dan Volume Group, pastikan ada 2 LVM PV dan VG &#8220;ejs&#8221; found disitu.<br /> <code>lvmdiskscan && vgscan</code><br /> 10. Cek kapasitas dari Volume Group &#8220;ejs&#8221;, pastikan ukurannya kurang lebih 15,99GB pada VG Size.<br /> <code>vgdisplay</code><br /> 11. Buatlah LVM Logical Volume dengan label home kapasitas 2GB.<br /> <code>lvcreate -L2G -n home ejs</code><br /> 12. Pastikan ukuran LSize / LV Size sebesar 2GB, LV Path pada /dev/ejs/home, pastikan juga status ACTIVE.<br /> <code>lvs && lvscan && lvdisplay</code><br /> 13. Sekarang Cek partisi yang telah dimount secara default, pastikan belum ada /home disitu.<br /> <code>df -ha</code><br /> 14. Selanjutnya buat file sistem Ext4 pada partisi yang baru dibuat pada /dev/ejs/home.<br /> <code>mkfs.ext4 /dev/ejs/home</code><br /> 15. Kemudian buatlah direktori pada /mnt/home_baru<br /> <code>mkdir /mnt/home_baru</code><br /> 16. Mounting lah /dev/ejs/home pada direktori baru tersebut.<br /> <code>mount /dev/mapper/ejs-home /mnt/home_baru</code><br /> 17. Cek kembali df -h, pastikan bahwa disitu ada /mnt/home_baru.<br /> <code>df -ha</code><br /> 18. Backuplah data pada /home dengan menggunakan resync.<br /> <code>rsync -av /home /mnt/home_baru</code><br /> 19. Selanjutnya umount partisi LVM tersebut.<br /> <code>umount /dev/mapper/ejs-home</code><br /> 20. Kemudian hapus folder default /home, pastikan setelah itu dibuat kembali folder /home.<br /> <code>rm -rf /home && mkdir /home</code><br /> 21. Selanjutnya mounting /dev/ejs/home ke direktori baru tersebut<br /> <code>mount /dev/mapper/ejs-home /home</code><br /> 22. Kemudian edit file pada fstab agar setiap kali di reboot, partisi tersebut otomatis di mount oleh sistem.<br /> <code>vi /etc/fstab</code><br /> 23. Kemudia cek konfigurasi fstab, pastikan statusnya adalah &#8220;already mounted&#8221;.<br /> <code>mount -av</code><br /> 24. Reboot<br /> 25. Kemudian setelah reboot, cek partisi df -h. Copykan folder atau apapun pada /home hingga use% sekitar 50%.<br /> 26. Gunakan rsync, scp atau winscp dari windows untuk copy, disini penulis ada server pada 10.101.3.149 dan ada akses ssh server disitu untuk mengambil data.<br /> <code>scp -pr root@10.101.3.149:/var/www/html/ /home/ekojs</code>
</p>

<p style="text-align: center;">
  <a href="https://ekojunaidisalam.com/wp-content/uploads/2016/03/partisi-awal.png" rel="attachment wp-att-182"><img class="aligncenter wp-image-182 size-full" src="https://ekojunaidisalam.com/wp-content/uploads/2016/03/partisi-awal.png" alt="/home penuh" width="675" height="424" srcset="https://ekojunaidisalam.com/wp-content/uploads/2016/03/partisi-awal.png 675w, https://ekojunaidisalam.com/wp-content/uploads/2016/03/partisi-awal-300x188.png 300w, https://ekojunaidisalam.com/wp-content/uploads/2016/03/partisi-awal-478x300.png 478w" sizes="(max-width: 675px) 100vw, 675px" /></a>
</p>

<p style="text-align: center;">
  ################# <strong>Cara Extend / Resize LVM Logical Volume</strong> #################
</p>

<p style="text-align: justify;">
  Pada kondisi ini partisi /home kapasitas 2GB telah penuh terisi 100%, diinginkan partisi tersebut di perbesar 10GB sehingga menjadi sekitar 12GB. Ikuti Prosedur berikut untuk melakukannya :<br /> 1. Cek terlebih dahulu Free Space pada LVM Physical Volume, pastikan cukup untuk resize sebesar 10GB.<br /> <code>pvs && pvscan</code><br /> 2. Cek partisi, pastikan size /home masih sekitar 2GB.<br /> <code>lvdisplay && df -h</code><br /> 2. Bila tersedia space yang dibutuhkan, lakukan extend pada /dev/ejs/home.<br /> <code>lvextend -L+10G /dev/ejs/home</code> Untuk mengakses seluruh freespace gunakan : <code>lvextend -l +100%FREE /dev/ejs/home</code><br /> 3. Pastikan LVM logical volume telah bertambah menjadi 12GB, dan pastikan pada partisi belum berubah.<br /> <code>lvs && lvscan && lvdisplay && df -h</code><br /> 4. Lho ???, kok di df -h masih sebesar 1,9GB ? Nah itu dia kita perlus me-resize file sistem ext4 pada /dev/ejs/home tersebut untuk benar &#8211; benar dapat menggunakan size penuh pada LVM Logical volume 12GB tersebut.<br /> <code>resize2fs /dev/ejs/home</code><br /> 5. Kemudia cek partisi kembali, pastikan size telah berubah dan Use % telah berkurang.<br /> <code>df -h</code><br /> 6. Taraaaa&#8230;. /home telah berubah menjadi berukuran 12GB, cek menggunakan pvscan seharusnya tersisa free space sebesar 3,9GB karena dari 16GB kepake 2GB tinggal 14GB diextend 10GB tinggal kurang lebih 4GB.
</p>

<p style="text-align: center;">
  <a href="https://ekojunaidisalam.com/wp-content/uploads/2016/03/lvextend.png" rel="attachment wp-att-183"><img class="aligncenter size-full wp-image-183" src="https://ekojunaidisalam.com/wp-content/uploads/2016/03/lvextend.png" alt="lvextend" width="675" height="424" srcset="https://ekojunaidisalam.com/wp-content/uploads/2016/03/lvextend.png 675w, https://ekojunaidisalam.com/wp-content/uploads/2016/03/lvextend-300x188.png 300w, https://ekojunaidisalam.com/wp-content/uploads/2016/03/lvextend-478x300.png 478w" sizes="(max-width: 675px) 100vw, 675px" /></a>
</p>

<p style="text-align: justify;">
  Selamat anda telah berhasil membuat konfigurasi LVM pada Centos 7, next Post bagaimana menggabungkan <strong>LVM + RAID10</strong> pada Centos 7. Jadi nantikan saja Artikelnya.
</p>
