---
id: 199
title: Membuat konfigurasi RAID1 + LVM pada RedHat (CentOS 7)
date: 2016-03-28T16:05:00+00:00
author: Eko Junaidi Salam
layout: post
guid: http://ekojunaidisalam.com/?p=199
permalink: /2016/03/28/konfigurasi-raid1-lvm-pada-redhat/
dsq_thread_id:
  - "4699217652"
dsq_needs_sync:
  - "1"
categories:
  - Artikel
  - Linux
  - Teknologi
  - 'Tip &amp; Trik'
tags:
  - Centos 7
  - LVM
  - lvm2
  - lvmdiskscan
  - mdadm
  - RAID
  - RAID Mirroring
  - RAID1
  - redhat
---
<h1 style="text-align: center;">
  <a href="{{site.baseurl}}/wp-content/uploads/2016/03/RAIDLVM.png" rel="attachment wp-att-200"><img class="aligncenter wp-image-200" src="{{site.baseurl}}/wp-content/uploads/2016/03/RAIDLVM-842x1024.png" alt="Konfigurasi RAID1" width="370" height="450" /></a>Konfigurasi RAID1 & LVM
</h1>

<p style="text-align: justify;">
  <strong>RAID</strong> (<strong><em>Redundancy Array of Inexpensive Disks</em></strong> atau sekarang dikenal dengan <em><strong>Redundant array of Independent Disks</strong></em>) adalah teknologi penyimpanan <em>virtual</em> yang menggabungkan beberapa <em>harddisk</em> (hdd) menjadi satu <em>logical disk unit</em>. Disini saya akan membahas Konfigurasi <strong>RAID1</strong> atau dikenal dengan <em><strong>RAID Mirroring</strong></em>.
</p>

<p style="text-align: justify;">
  <em><strong>RAID Mirroring</strong></em> (<strong>RAID1</strong>) adalah Teknologi RAID yang memerlukan paling sedikit 2 hdd untuk bisa membuat disk <em>mirror </em>(<em>clone</em>) dimana data ditulis sama pada kedua hdd. Konfigurasi ini memungkinkan untuk mencegah <em>data loss</em> saat <em>disk fail</em>, karena data benar &#8211; benar ditulis sama pada kedua disk. Karena RAID1 adalah <em>RAID Mirroring</em> maka hdd hanya akan terbaca 50% dari jumlah <em>size</em> hdd, contoh bila kita punya 2 disk dengan ukuran 500GB seharusnya jumlah total 1TB tapi karena <em>mirror</em> maka hdd hanya akan terbaca 500GB.
</p>

<p style="text-align: justify;">
  Selanjutnya setelah konfigurasi <strong>RAID1</strong> selesai kita lakukan, maka kita akan menempatkan <strong>LVM</strong> diatas <strong>RAID1</strong> tersebut. Beberapa user sempat menanyakan &#8220;<strong>LVM diatas RAID (mdadm) atau RAID (mdadm) diatas LVM ?</strong>&#8220;, mengenai LVM baca artikel &#8220;<a href="{{site.baseurl}}/2016/03/05/konfigurasi-lvm-pada-linux-centos-7/" target="_blank"><em><strong>Membuat Konfigurasi LVM pada Linux (CentOS 7)</strong></em></a>&#8220;. Secara singkat <strong>LVM</strong> adalah software mapper pada <em>kernel linux</em> yang digunakan untuk <em>mapping</em> beberapa <em>harddisk</em> menjadi satu atau beberapa <em>Volume Group</em> agar flexible saat <strong><em>Extend</em></strong> maupun <em><strong>Resize</strong> </em>baca (<strong>E-R</strong>) pada <em>Logical Volume</em> yang telah dibuat. Sedangkan <strong>RAID</strong> adalah teknologi penyimpanan <em>virtual</em> yang menggabungkan beberapa hdd baik secara <em>software</em> menggunakan <em><strong>mdadm</strong> </em>ataupun <em><strong>HW RAID</strong></em>. Dimana proses <strong>E-R</strong> pada <strong>RAID</strong> bergantung dimana konfigurasi itu dibuat, apakah dikonfigurasi secara <em>software</em> menggunakan <em><strong>mdadm</strong> </em>ataukah langsung dari <em><strong>HW RAID</strong></em>.<a name='more'></a>
</p>

<p style="text-align: justify;">
  Konfigurasi <em><strong>RAID non LVM</strong></em>, misalkan RAID1 memiliki fungsi untuk menangani <em>Disk Failure</em> pada salah satu <em>disk</em> yang rusak sehingga dengan kondisi tersebut sistem masih tetap bisa berjalan dengan semestinya. Namun bila <strong>RAID1</strong> ada diatas konfigurasi <strong>LVM</strong>, maka kegagalan pada salah satu hdd yang dimapping oleh LVM menyebabkan kegagalan seluruh sistem sehingga konfigurasi <strong>RAID1 diatas LVM</strong> menjadi <strong>tidak berguna</strong>. Lain halnya bila Konfigurasi LVM diatas konfigurasi RAID1, karena <em>disk</em> yang di<em>mapping</em> oleh LVM adalah disk yang telah dikonfigurasi oleh RAID1 misalkan pada <em><strong>/dev/md0</strong></em> sehingga apabila terjadi kegagalan hdd pada salah satu RAID1 tidak menyebabkan kegagalan seluruh sistem karena fungsi <em>mirroring</em>(<em>clone</em>) dari RAID1 tersebut.
</p>

<p style="text-align: justify;">
  <strong>Kesimpulannya</strong>, konfigurasi yang <em><strong>direkomendasikan</strong> </em>oleh penulis adalah menempatkan <strong>LVM diatas RAID</strong>. Mari kita lihat bagaimana prosedur konfigurasinya.
</p>

<p style="text-align: justify;">
  <strong>BACKUP</strong> segela konfigurasi bila dilakukan dalam live server, kegagalan yang terjadi akibat mengikuti prosedur dibawah <strong>BUKAN</strong> tanggung jawab penulis. Langkah &#8211; langkahnya adalah sebagai berikut :<br /> 1. Cek informasi pada disk. Gambar dibawah adalah screen shot konfigurasi normal setelah instalasi CentOS 7.
</p>

<pre class="lang:sh decode:true" title="Cek informasi disk">df -h
cat /proc/mdstat
lvmdiskscan</pre>

<p style="text-align: justify;">
  <a href="{{site.baseurl}}/wp-content/uploads/2016/03/RAID0.png" rel="attachment wp-att-202"><img class="aligncenter size-full wp-image-202" src="{{site.baseurl}}/wp-content/uploads/2016/03/RAID0.png" alt="RAID0" width="675" height="424" srcset="{{site.baseurl}}/wp-content/uploads/2016/03/RAID0.png 675w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID0-300x188.png 300w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID0-478x300.png 478w" sizes="(max-width: 675px) 100vw, 675px" /></a>2. Tambahkan 2 disk baru untuk konfigurasi RAID1, kemudian cek.
</p>

<pre class="lang:default decode:true" title="Menambahkan 2 Disk baru untuk RAID1">ls /dev/sd*
mdadm -E /dev/sd[b-c]
fdisk -l /dev/sd[b-c]</pre>

<p style="text-align: justify;">
  <a href="{{site.baseurl}}/wp-content/uploads/2016/03/RAID1.png" rel="attachment wp-att-203"><img class="aligncenter size-full wp-image-203" src="{{site.baseurl}}/wp-content/uploads/2016/03/RAID1.png" alt="RAID1" width="675" height="424" srcset="{{site.baseurl}}/wp-content/uploads/2016/03/RAID1.png 675w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID1-300x188.png 300w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID1-478x300.png 478w" sizes="(max-width: 675px) 100vw, 675px" /></a>3. Kemudian buatlah Partition Type Linux raid autodetect, seperti tampilan dibawah.
</p>

<p style="text-align: justify;">
  <a href="{{site.baseurl}}/wp-content/uploads/2016/03/RAID2.png" rel="attachment wp-att-204"><img class="aligncenter size-full wp-image-204" src="{{site.baseurl}}/wp-content/uploads/2016/03/RAID2.png" alt="RAID2" width="675" height="424" srcset="{{site.baseurl}}/wp-content/uploads/2016/03/RAID2.png 675w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID2-300x188.png 300w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID2-478x300.png 478w" sizes="(max-width: 675px) 100vw, 675px" /></a>4. Setelah itu buatlah RAID1 pada disk /dev/sdb1 dan /dev/sdc1
</p>

<pre class="lang:default decode:true" title="Membuat RAID Level 1">mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sd[b-c]1</pre>

<p style="text-align: justify;">
  <a href="{{site.baseurl}}/wp-content/uploads/2016/03/RAID3.png" rel="attachment wp-att-205"><img class="aligncenter size-full wp-image-205" src="{{site.baseurl}}/wp-content/uploads/2016/03/RAID3.png" alt="RAID3" width="675" height="424" srcset="{{site.baseurl}}/wp-content/uploads/2016/03/RAID3.png 675w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID3-300x188.png 300w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID3-478x300.png 478w" sizes="(max-width: 675px) 100vw, 675px" /></a>5. Cek RAID1 yang telah dibuat tadi.
</p>

<pre class="lang:default decode:true" title="Cek RAID Level 1">cat /proc/mdstat
mdadm --detail /dev/md0</pre>

<p style="text-align: justify;">
  <a href="{{site.baseurl}}/wp-content/uploads/2016/03/RAID4.png" rel="attachment wp-att-206"><img class="aligncenter size-full wp-image-206" src="{{site.baseurl}}/wp-content/uploads/2016/03/RAID4.png" alt="RAID4" width="675" height="424" srcset="{{site.baseurl}}/wp-content/uploads/2016/03/RAID4.png 675w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID4-300x188.png 300w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID4-478x300.png 478w" sizes="(max-width: 675px) 100vw, 675px" /></a>6. Setelah proses resyncing pada kedua disk RAID selesai, buatlah Physical Volume dan Volume Group untuk membuat LVM diatas RAID.
</p>

<pre class="lang:default decode:true" title="Membuat Lingkungan LVM">pvcreate /dev/md0
vgcreate ejs /dev/md0
pvs
vgs</pre>

<p style="text-align: justify;">
  <a href="{{site.baseurl}}/wp-content/uploads/2016/03/RAID5.png" rel="attachment wp-att-207"><img class="aligncenter size-full wp-image-207" src="{{site.baseurl}}/wp-content/uploads/2016/03/RAID5.png" alt="RAID5" width="675" height="424" srcset="{{site.baseurl}}/wp-content/uploads/2016/03/RAID5.png 675w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID5-300x188.png 300w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID5-478x300.png 478w" sizes="(max-width: 675px) 100vw, 675px" /></a>7. Kemudian buatlah Logical Volume ukuran 3GB dengan label home pada Volume Group ejs. Kemudian simpan konfigurasi mdadm tersebut dan buat File System ext4 pada Logical Volume yang telah dibuat.
</p>

<pre class="lang:default decode:true " title="Membuat Logical Volume pada RAID 1">lvcreate -L3G -n home ejs
mdadm --detail --scan --verbose &gt; /etc/mdadm.conf
mkfs.ext4 /dev/ejs/home</pre>

<p style="text-align: justify;">
  <a href="{{site.baseurl}}/wp-content/uploads/2016/03/RAID6.png" rel="attachment wp-att-208"><img class="aligncenter size-full wp-image-208" src="{{site.baseurl}}/wp-content/uploads/2016/03/RAID6.png" alt="RAID6" width="1366" height="738" srcset="{{site.baseurl}}/wp-content/uploads/2016/03/RAID6.png 1366w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID6-300x162.png 300w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID6-768x415.png 768w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID6-1024x553.png 1024w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID6-500x270.png 500w" sizes="(max-width: 1366px) 100vw, 1366px" /></a>8. Logical Volume telah dibuat, sekarang waktunya me-mounting /dev/ejs/home ke /mnt/home misalkan.
</p>

<pre class="lang:default decode:true " title="Mounting Logical Volume yg telah dibuat">mkdir /mnt/home
mount /dev/mapper/ejs-home /mnt/home
df -h</pre>

<p style="text-align: justify;">
  9. Bila ingin membuat /home ada pada partisi LVM ejs-home tersebut, maka data perlu disalin dan restorecon pada /home hasil mapper /dev/mapper/ejs-home tersebut agar SELinux Security contexts kembali ke contexts default.
</p>

<pre class="lang:default decode:true " title="Konfigurasi SELinux Security dan fstab">scp -pr /home/ /mnt/
umount /mnt/home
mount /dev/mapper/ejs-home /home
cd /home
restorecon /home/
df -h
echo "/dev/mapper/ejs-home /home ext4 defaults 0 0" &gt;&gt; /etc/fstab
mount -av
lsblk</pre>

<p style="text-align: justify;">
  <a href="{{site.baseurl}}/wp-content/uploads/2016/03/RAID7.png" rel="attachment wp-att-209"><img class="aligncenter size-full wp-image-209" src="{{site.baseurl}}/wp-content/uploads/2016/03/RAID7.png" alt="RAID7" width="675" height="424" srcset="{{site.baseurl}}/wp-content/uploads/2016/03/RAID7.png 675w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID7-300x188.png 300w, {{site.baseurl}}/wp-content/uploads/2016/03/RAID7-478x300.png 478w" sizes="(max-width: 675px) 100vw, 675px" /></a>10. Selesai
</p>
