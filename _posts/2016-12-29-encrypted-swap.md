---
id: 304
title: Encrypted Swap menggunakan LUKS Encryption pada Ubuntu
date: 2016-12-29T07:10:32+00:00
author: Eko Junaidi Salam
layout: post
guid: http://ekojunaidisalam.com/?p=304
permalink: /2016/12/29/encrypted-swap/
dsq_thread_id:
  - "5418181862"
categories:
  - Artikel
  - Linux
  - Programming
  - 'Tip &amp; Trik'
tags:
  - bash
  - bug
  - debian
  - Encrypted Swap
  - Linux
  - LUKS
  - LUKS Encryption
  - matikan
  - swap
  - ubuntu
---
<h2 style="text-align: center;">
  <a href="https://ekojunaidisalam.com/wp-content/uploads/2016/12/swap_bug.png"><img class="aligncenter wp-image-305 size-full" src="https://ekojunaidisalam.com/wp-content/uploads/2016/12/swap_bug.png" alt="Encrypted Swap" width="732" height="227" srcset="https://ekojunaidisalam.com/wp-content/uploads/2016/12/swap_bug.png 732w, https://ekojunaidisalam.com/wp-content/uploads/2016/12/swap_bug-300x93.png 300w, https://ekojunaidisalam.com/wp-content/uploads/2016/12/swap_bug-500x155.png 500w" sizes="(max-width: 732px) 100vw, 732px" /></a>Encrypted Swap menggunakan LUKS Encryption
</h2>

<p style="text-align: justify;">
  Dua hari yang lalu saya dibuat kaget dengan tidak terbacanya <strong>swap</strong> saat melakukan pengecekan menggunakan <span class="lang:default decode:true crayon-inline ">free -h</span>&nbsp;. Seperti terlihat di gambar, swap saya total <strong>0B</strong> yang seharusnya sekitar <strong>8GB</strong>. Ketika saya cek <em>crypttab</em> dan <em>fstab</em> semua tidak ada masalah, namun ketika saya cek blkid, saya kaget setengah sadar 😀 UUID pada partisi saya yang <span class="lang:default decode:true crayon-inline ">/dev/sda6</span>&nbsp; hanya berisi <strong>PARTUUID</strong> tanpa <strong>UUID</strong>, saya cari-cari di device tidak ada UUID yang tersimpan pada <em>crypttab</em>. Kebetulan saya memasang Encrypted Swap menggunakan LUKS Encryption begitu juga dengan beberapa partisi pada laptop saya.
</p>

<p style="text-align: justify;">
  Usut demi usut, setelah saya obrak-abrik mbah gugel saya menemukan informasi yang valid yang mengatakan bahwa kondisi itu adalah bug yang belum dipatch dari ubuntu 14.04 dan sampai dengan ubuntu 16.04 hal tersebut masih akan terjadi. Saya sampe obrak-abrik gugel karena hal ini terjadi 2 kali, uda rebuildnya lumayan eh hilang mulu swapnya.<a name='more'></a>
</p>

<p style="text-align: justify;">
  <a href="https://ekojunaidisalam.com/wp-content/uploads/2016/12/swap_bug_fix.png"><img class="aligncenter size-full wp-image-306" src="https://ekojunaidisalam.com/wp-content/uploads/2016/12/swap_bug_fix.png" alt="Encrypted Swap" width="675" height="257" srcset="https://ekojunaidisalam.com/wp-content/uploads/2016/12/swap_bug_fix.png 675w, https://ekojunaidisalam.com/wp-content/uploads/2016/12/swap_bug_fix-300x114.png 300w, https://ekojunaidisalam.com/wp-content/uploads/2016/12/swap_bug_fix-500x190.png 500w" sizes="(max-width: 675px) 100vw, 675px" /></a>Sekarang swap saya sudah aman lagi, cuma bukan karena sudah aman trus saya menulis artikel ini. Tapi lebih kepada bila ada teman-teman pembaca yang juga mengalami hal yang serupa dapat mencoba solusi yang sudah terbukti ampuh ini. Karena delik masalah yang agak ruwet, akhirnya saya buatkan program kecil <a href="https://github.com/ekojs/matikan" target="_blank">disini </a>untuk melakukan soft <em>reboot/shutdown</em> bisa juga untuk <strong><em>rebuilding</em> </strong><em>Encrypted Swap</em> yang hilang entah kenapa. Seluruh proses telah diuji, bahkan pada laptop pribadi penulis (saya) 😀 .
</p>

<p style="text-align: justify;">
  Namun, untuk tetap <strong>selalu</strong> diingat. Segala bentuk kerusakan yang mungkin ditimbulkan karena mengikuti petunjuk pada postingan ini, sepenuhnya menjadi resiko anda sendiri, <strong>BUKAN</strong> <strong>tanggung jawab</strong> penulis. Bila ada diskusi monggo <em>comment. </em>😀
</p>

Berikut Cara Membuat Encrypted Swap menggunakan LUKS Encryption :

<pre class="lang:default decode:true " title="Membuat Encrypted Swap menggunakan LUKS">1. sudo cryptsetup --verbose --verify-passphrase luksFormat /dev/sda6
2. sudo cryptsetup luksOpen /dev/sda6 sda6_crypt
3. sudo mkswap -L swap /dev/mapper/sda6_crypt
Gunakan UUID pada partisi untuk digunakan pada /etc/crypttab
Data UUID untuk partisi /dev/sda6
UUID="b39babff-ccfb-47d2-bef7-576783659381"

Cek blkid
4. sudo blkid
ekojs@ekojs-laptop:~$ sudo blkid
/dev/sda1: UUID="fcb1ff57-fbfe-4f5d-82bf-fc372cf53904" TYPE="ext4" PARTUUID="2ba375fb-01"
/dev/sda2: UUID="e87c4cc9-81cb-46ae-892d-15f6b1977bbc" TYPE="ext4" PARTUUID="2ba375fb-02"
/dev/sda5: UUID="59a8a751-8f78-49ad-81ac-383f6870588c" TYPE="crypto_LUKS" PARTUUID="2ba375fb-05"
/dev/sda6: UUID="b39babff-ccfb-47d2-bef7-576783659381" TYPE="crypto_LUKS" PARTUUID="2ba375fb-06"

5. sudo vim /etc/crypttab
#sda6_crypt UUID=5b154575-4677-4573-8f97-80664da5b864 none luks,swap,discard
sda6_crypt UUID=b39babff-ccfb-47d2-bef7-576783659381 none luks,swap,discard

Tambahkan entri untuk swap bila belum ada
6. sudo vim /etc/fstab
/dev/mapper/sda6_crypt none swap sw 0 0

Kemudian di test dengan menjalankan cryptdisks_start
7. sudo swapoff -a
8. sudo cryptsetup luksClose sda6_crypt
9. sudo cryptdisks_start sda6_crypt

Aktifkan Swap
10. sudo swapon -a
11. free -h

Nonaktifkan Swap
12. sudo swapoff -a
13. free -h
14. sudo cryptsetup luksClose sda6_crypt

Terakhir Update Initramfs
15. sudo update-initramfs -u -k all</pre>

<p style="text-align: justify;">
  Petunjuk diatas juga dapat digunakan bila akan merebuild ulang swap yang hilang atau rusak. Untuk lebih jelas dan detail dari program yang saya berikan di postingan ini, dapat langsung di baca di github <a href="https://github.com/ekojs/matikan" target="_blank">https://github.com/ekojs/matikan</a>.
</p>

<p style="text-align: justify;">
  Lha terus, dimana penyelesaian dari bug yang ditimbulkan ? tenang bro kita sampai kesana nanti. Sekarang mari cermati bugnya terlebih dahulu di link <a href="https://bugs.launchpad.net/ubuntu/+source/ecryptfs-utils/+bug/1310058" target="_blank">bug ubuntu 14.04</a>. Bila teman-teman pembaca juga memiliki masalah yang sama dengan bug tersebut, silahkan cek <a href="https://bugs.launchpad.net/ubuntu/+source/ecryptfs-utils/+bug/1310058/+affectsmetoo" target="_blank">link ini</a> dan vote yes agar bug ini bisa menjadi perhatian bagi temen-temen developer.
</p>

<p style="text-align: justify;">
  Oke, sudah dibaca link bugnya ? sampai selesai kan ? Oke, menurut <a href="https://launchpad.net/~albertpool" target="_blank">Albert Pool</a> bug tersebut menyebabkan UUID pada swap partition menjadi tidak terbaca, kemudia setelah dia melakukan testing dia menemukan solusi bahwa menambahkan &#8220;<em><strong>offset=8</strong></em>&#8221; dapat menyelesaikan bug tersebut. Kemudian dibeberapa komentar ada yang memberikan solusi agak lengkap yang berkenaan juga dengan &#8220;<em><strong>offset=8</strong></em>&#8221; oleh wetware.
</p>

<p style="text-align: justify;">
  Merasa kurang dari pembahasan bug tersebut teman-teman pembaca dapat membaca&nbsp; <a href="https://bugs.launchpad.net/ubuntu/+source/ecryptfs-utils/+bug/953875" target="_blank">link bug</a> berikut yang lebih mengena dalam permasalahan bahwa swap tidak otomatis termounted saat booting. Dari pembahasan inilah akhirnya saya dapat membuat program kecil yang sesuai dengan permasalahan saya dan juga tools yang saya gunakan untuk mengenkripsi swap. Ternyata setelah dites penggunaan &#8220;offset=8&#8221; bisa menyelesaikan bug tersebut, meski beberapa ada yang mengatakan penggunaan &#8220;offset=1024&#8221; begitu juga dengan offset kelipatan 512 juga berhasil, namun itu semua perlu disesuaikan.
</p>

<p style="text-align: justify;">
  <a href="https://ekojunaidisalam.com/wp-content/uploads/2016/12/matikan.png"><img class="aligncenter size-full wp-image-307" src="https://ekojunaidisalam.com/wp-content/uploads/2016/12/matikan.png" alt="matikan" width="450" height="517" srcset="https://ekojunaidisalam.com/wp-content/uploads/2016/12/matikan.png 450w, https://ekojunaidisalam.com/wp-content/uploads/2016/12/matikan-261x300.png 261w" sizes="(max-width: 450px) 100vw, 450px" /></a>Berikut adalah tampilan help pada program kecil yang saya buat, program tersebut dibuat untuk dapat melakukan swapon/off secara manual, soft poweroff/reboot dan rebuild Encrypted Swap yang hilang atau rusak. Begitu juga solusi dari pembahasan bug diatas sudah saya terapkan pada program kecil ini.
</p>

<p style="text-align: justify;">
  Akhir kata, semoga artikel kali ini dapat bermanfaat bagi teman-teman pembaca. Bila ada yang perlu didiskusikan, silahkan email ataupun koment. 😀
</p>
