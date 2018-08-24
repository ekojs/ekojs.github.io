---
id: 275
title: Migrasi antar Hosting Cpanel
date: 2016-12-12T19:48:05+00:00
author: Eko Junaidi Salam
layout: post
guid: http://ekojunaidisalam.com/?p=275
permalink: /2016/12/12/migrasi-antar-hosting/
dsq_thread_id:
  - "5374316284"
dsq_needs_sync:
  - "1"
categories:
  - Artikel
  - Teknologi
  - 'Tip &amp; Trik'
tags:
  - cpanel
  - domain
  - hosting
  - Kode EPP
  - migrasi hosting
  - server
  - transfer domain
---
<div style="text-align: center;"><img src="{{site.baseurl}}/wp-content/uploads/2016/12/migration-servers.png" /></div>
<h2 style="text-align: center;">Migrasi antar Hosting</h2>

<p style="text-align: justify;">
  Setelah beberapa hari website ini down karena habis masa sewa <em>hosting</em> dan domainnya, sekarang <em>website</em> ini kembali online, setelah penulis melakukan Migrasi antar Hosting yang berbeda. 😀
</p>

<p style="text-align: justify;">
  Beberapa hari lalu saat <em>website</em> ini down, penulis sedang melakukan migrasi <em>hosting</em> dan <em>backup-restore</em> dari <em>hosting</em> lama. Lumayan melakukan <em>reconfigure</em> dan <em>restore</em> data ke lokasi <em>hosting</em> baru.
</p>

<p style="text-align: justify;">
  Paling tidak postingan kali ini dapat menjadi acuan teman-teman pembaca dalam melakukan migrasi antar <em>hosting</em> berbeda saat dibutuhkan nanti. Berikut cara melakukan migrasi <em>hosting</em> pada <em>server</em> <em>apache/mysql</em> dengan control panel <em><strong>CPANEL</strong></em>.
</p>

<p style="text-align: justify;">
  <span style="text-decoration: underline;"><strong>Sebagai catatan</strong></span>, pastikan saat akan melakukan migrasi <em>hosting</em> dan <em>transfer</em> <em>domain</em> harus cocok (tipe <em>server</em>, <em>database</em>, <em>cpanel</em>). Namun bukan berarti bila ada yg berbeda kita tidak bisa melakukan migrasi, melakukan migrasi yang berbeda dari sumbernya membutuhkan perlakuan dan waktu <em><strong>extra</strong></em>.
</p>

<p style="text-align: justify;">
  Segala bentuk kerusakan yang mungkin ditimbulkan karena mengikuti petunjuk pada postingan ini, sepenuhnya menjadi resiko anda sendiri, <strong>BUKAN</strong> <strong>tanggung jawab</strong> penulis. Bila ada diskusi monggo <em>comment</em>.
</p>

<p style="text-align: center;">
  <a href="{{site.baseurl}}/wp-content/uploads/2016/12/isi-backup.png"><img class="aligncenter size-large wp-image-281" src="{{site.baseurl}}/wp-content/uploads/2016/12/isi-backup-1024x325.png" alt="Hasil Backup" height="185" width="584" srcset="{{site.baseurl}}/wp-content/uploads/2016/12/isi-backup-1024x325.png 1024w, {{site.baseurl}}/wp-content/uploads/2016/12/isi-backup-300x95.png 300w, {{site.baseurl}}/wp-content/uploads/2016/12/isi-backup-768x244.png 768w, {{site.baseurl}}/wp-content/uploads/2016/12/isi-backup-500x159.png 500w, {{site.baseurl}}/wp-content/uploads/2016/12/isi-backup.png 1450w" sizes="(max-width: 584px) 100vw, 584px" /></a>Hasil <em>extract</em> file <strong>backup-8.17.2016_19-38-16_username.tar.gz</strong><a name='more'></a>
</p>

<p style="text-align: justify;">
  Langkah &#8211; langkah melakukan migrasi antar hosting yang berbeda :
</p>

<li style="text-align: justify;">
  Bila anda perlu <em>transfer domain</em>, maka anda perlu <em><strong>kode EPP</strong></em>, untuk melakukannya.
</li>
<li style="text-align: justify;">
  Lakukan <em>full backup</em> melalui <em>cpanel</em> anda pada modul <em><strong>Files</strong> </em>&#8211; <em><strong>Download a Full Website Backup</strong></em>, isikan <em>email</em> untuk notifikasi kemudian <em>generate</em>.
</li>
<li style="text-align: justify;">
  Setelah ada notif pada <em>email</em> bila <em>backup</em> telah selesai, file berekstensi <strong>*.tar.gz</strong> akan berada pada <em>home directory</em> anda. <em>Download</em> file tersebut ke komputer lokal.
</li>
<li style="text-align: justify;">
  Lakukan <em>reconfigure</em> pada hasil backup tersebut dengan melakukan <em>extract</em> terlebih dahulu. Dengan parameter konfigurasi : <ol>
    <li style="text-align: justify;">
      <em>Username</em> cpanel perlu dicatat, beberapa menggunakan <em>username</em> sebagai home dir.
    </li>
    <li style="text-align: justify;">
      Lokasi <em>path home directory</em> perlu dicatat.
    </li>
    <li style="text-align: justify;">
      <em>Username</em> dan <em>password</em> <strong>MySQL</strong> serta nama <strong>Database</strong>.
    </li>
    <li style="text-align: justify;">
      <strong>IP Address</strong> pada hosting (<em>Shared IP Address</em>).
    </li>
    <li style="text-align: justify;">
      <strong>DKIM</strong>, <em>ssh key</em>, <em>gpg key</em>, dan otentikasi lainnya.<br /> <em>Reconfigure</em> ini dilakukan dengan <strong>menyesuaikan</strong> (<em>replace</em>) pengaturan hosting baru dengan hosting lama.<br /> <a href="{{site.baseurl}}/wp-content/uploads/2016/12/contoh.png"><img class="aligncenter size-full wp-image-279" src="{{site.baseurl}}/wp-content/uploads/2016/12/contoh.png" alt="Modul cpanel" height="740" width="466" srcset="{{site.baseurl}}/wp-content/uploads/2016/12/contoh.png 466w, {{site.baseurl}}/wp-content/uploads/2016/12/contoh-189x300.png 189w" sizes="(max-width: 466px) 100vw, 466px" /></a>
    </li>
  </ol>
</li>

<li style="text-align: justify;">
  <em>Setting up</em> modul terlebih dahulu sebelum <em>home directory</em>, seperti : <ol>
    <li style="text-align: justify;">
      Modul <strong><em>database</em></strong>, <em>import</em> <em>database</em> website dan email (<em>roundcube</em> biasanya).
    </li>
    <li style="text-align: justify;">
      Modul <strong><em>domains</em></strong>, isikan pengaturan pada <em>subdomain</em>, <em>aliases</em>, <em>redirects</em>, dan <em>advanced zone editor</em>.
    </li>
    <li style="text-align: justify;">
      Modul <strong><em>emails</em></strong>, setting <em>mx entry</em>, <em>encryption</em>, import <em>authentication</em>, dkim, spf dan alamat email.
    </li>
    <li style="text-align: justify;">
      Modul <strong><em>security</em></strong>, setting <em>ssl/tls</em>,<em> ip blocker</em>, dan <em>hotlink protector</em>.<br /> <a href="{{site.baseurl}}/wp-content/uploads/2016/12/contoh-1.png"><img class="aligncenter size-full wp-image-280" src="{{site.baseurl}}/wp-content/uploads/2016/12/contoh-1.png" alt="Modul Security Cpanel" height="118" width="478" srcset="{{site.baseurl}}/wp-content/uploads/2016/12/contoh-1.png 478w, {{site.baseurl}}/wp-content/uploads/2016/12/contoh-1-300x74.png 300w" sizes="(max-width: 478px) 100vw, 478px" /></a>
    </li>
  </ol>
</li>

<li style="text-align: justify;">
  <em>Replace</em> homedir/public_html dengan public_html yang lama. Tunggu hingga proses <em>copy</em> selesai dilakukan.
</li>
<li style="text-align: justify;">
  Testing web.
</li>

Proses Migrasi anda telah berhasil dilakukan, bila ada proses yang mengalami kegagalan atau tidak berjalan sebagaimana mestinya anda dapat berkomentar dibawah ini dengan menyertai pesan kesalahan yand ditimbulkan. Semoga bermanfaat.
