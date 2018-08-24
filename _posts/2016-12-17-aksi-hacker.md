---
id: 292
title: Aksi Hacker pada ekojunaidisalam.com
date: 2016-12-17T01:14:34+00:00
author: Eko Junaidi Salam
layout: post
guid: http://ekojunaidisalam.com/?p=292
permalink: /2016/12/17/aksi-hacker/
dsq_thread_id:
  - "5385615481"
dsq_needs_sync:
  - "1"
categories:
  - Artikel
  - Teknologi
tags:
  - backdoor
  - hacking
  - shellcode
  - xaishell
---
![aksi-hacker-1](/wp-content/uploads/2016/12/diretas.png)
<h2 style="text-align: center;">Aksi Hacker</h2>

<p style="text-align: justify;">
  Aksi Hacker kali ini membuat website <a href="https://ekojunaidisalam.com/" target="_blank">ekojunaidisalam.com</a>, sempat down gara-gara seorang hacker dengan alias <strong>Rinto AR</strong> dari <em><strong>XaiSyndicate</strong></em>. Dia menggunakan celah pada wordpress untuk menanam <em>backdoor</em> pada website saya. Dengan bantuan tools <em>shellcode</em> dengan <strong>IP 159.253.145.183</strong> jam server <strong>[15/Dec/2016:12:01:25]</strong> dia mengakses url &#8220;<strong><a href="http://astaga.id/upload/images/coba.php?dir=/home/k7119888/public_html/upload/images/xai_config&do=auto_edit_user" target="_blank">http://astaga.id/upload/images/coba.php?dir=/home/k7119888/public_html/upload/images/xai_config&do=auto_edit_user</a></strong>&#8221; yang mungkin dia gunakan untuk mempersiapkan persenjataan untuk mendeface website saya. Setelah melakukan berbagai macam upaya untuk mengupload plugin khusus yang dia <em>recoded</em> untuk menanam <em>backdoor</em>, yang ternyata setelah sukses pluginnya membuat direktori bernama &#8220;<strong>santet</strong>&#8220;. Dia melakukan pencarian terhadap hasil instalasi plugin yang berisi backdoor tersebut, terlihat ketika saya melakukan tracing terhadap aktivitasnya.
</p>

<p style="text-align: justify;">
  <a href="{{site.baseurl}}/wp-content/uploads/2016/12/shellcode.png"><img class="aligncenter size-full wp-image-294" src="{{site.baseurl}}/wp-content/uploads/2016/12/shellcode.png" alt="Aksi Hacker" width="794" height="630" srcset="{{site.baseurl}}/wp-content/uploads/2016/12/shellcode.png 794w, {{site.baseurl}}/wp-content/uploads/2016/12/shellcode-300x238.png 300w, {{site.baseurl}}/wp-content/uploads/2016/12/shellcode-768x609.png 768w, {{site.baseurl}}/wp-content/uploads/2016/12/shellcode-378x300.png 378w" sizes="(max-width: 794px) 100vw, 794px" /></a><a name='more'></a>Alhasil setelah jam 
  
  <strong>[15/Dec/2016:12:12:50]</strong> dengan IP yang sama dia menemukan plugin yang sudah dia install di &#8220;<strong>/wp-content/plugins/santet/</strong>&#8220;, dimana ternyata disitu berisi <em>backdoor</em> bernama &#8220;<strong>xaishell.php</strong>&#8221; yang ketika saya <em>traceback</em> dan berhasil mendapatkan <em>code script</em> yang dia gunakan untuk melakukan <em>WordPress Auto Deface</em>, <em>Auto Edit User</em>, <em>Adminer</em>,<em> Bypass vHost</em>, kurang lebih ada 43 modul untuk meretas yang saya lihat pada <em>code script</em> tersebut. Anehnya pada jam <strong>[15/Dec/2016:12:36:41]</strong> dengan IP baru <strong>36.72.207.219</strong> dia mengupload file ke &#8220;<strong>/wp-content/uploads/2016/12/encode.php</strong>&#8221; yang dengan itu juga dia melakukan deface pada file<em><strong> index.php</strong></em> website saya.
</p>

<p style="text-align: justify;">
  Tepat jam <strong>[15/Dec/2016:12:37:03]</strong>, dia selesai melakukan akses ke file &#8220;<strong>encode.php</strong>&#8220;. Setelah dia mengobok-obok database user saya dengan mengganti <em>username</em> dan <em>password</em>, dia melakukan login dengan mulus ke website saya dengan username saat itu &#8220;<strong>syndicate</strong>&#8220;, kemudian entah kenapa sekitar 30 menitan dia mengganti username menjadi &#8220;<strong>rintoar</strong>&#8221; dengan password &#8220;<strong>rintoar2234</strong>&#8221; dengan IP yang sebenarnya bisa saya trace hingga ke lokasi dimana dia melakukan tindakan peretasan ini. Yang bila mereka membaca <strong>UU ITE Nomor 11 Th 2008 pasal 46 ayat 1</strong> minimal mereka di <strong>pidana penjara</strong> paling lama <strong>6 tahun</strong> dan/atau <strong>denda</strong> paling banyak <strong>Rp. 600.000.000,00</strong> (enam ratus juta rupiah).
</p>

<p style="text-align: justify;">
  Sebenarnya saya senang sekali ada hacker yang mengobok2 website saya, <strong>tanya</strong> mengapa ? Ya iyalah senang mas/mbak pembaca, kita di <a href="https://hackerone.com/" target="_blank"><strong>hackerone.com</strong></a> ketika menemukan bug pada sebuah sistem kita dibayar mahal mulai dari <strong>$500</strong> hingga <strong>ribuan dollar</strong> demi mencari celah seperti misal pada situs <strong><em>instagram</em></strong>, <strong><em>imgur</em></strong>, dll :D. Nah ini hacker dengan baik hati mencari bug pada website saya yang sebenarnya sudah banyak yang mempublish <em><strong>POC</strong> </em>(<em><strong>Proof Of Concept</strong></em>) bug pada wordpress seperti di <a href="https://www.pluginvulnerabilities.com/blog/" target="_blank"><strong>https://www.pluginvulnerabilities.com/blog/</strong></a> yang bisa teman-teman pembaca akses. Disitu dijelaskan ada beberapa <em>issue</em> yang sebenarnya sudah lama, namun belum dilakukan perbaikan/tanggapan terhadap bug itu.
</p>

<p style="text-align: justify;">
  Sekarang website saya telah kembali ke kondisi seperti semula, sekali lagi saya sangat senang sekali bila ada hacker dengan baik hati meretas website saya. Karena disatu sisi saya menggunakan wordpress yang notabene banyak jadi sasaran aksi hacker, kedua saya males baca-baca bug terkini, jadi bila ada yang menghack website saya itu berarti saat itu saya harus melakukan <em>patching</em> pada bug tersebut, paling tidak saya tak perlu rajin mengecek bug terkini di wordpress hehe 😀 .
</p>

<p style="text-align: justify;">
  Saran saya terhadap teman-teman pembaca yang mungkin juga memiliki website, agar selalu <em>backup</em> dibanyak tempat, di local, di <em>cloud</em>, dan dimana saja bisa dibackup. Sehingga bila terjadi kerusakan yang diakibatkan oleh orang yang tak bertanggung jawab, bisa dapat kita selamatkan. Sebenarnya backup saja tidak cukup, kalau kita mampu memodifikasi <em>source code</em> corenya kenapa kita tidak implant <em>backtrack</em> pada beberapa file yang pantas di jadikan umpan 😀 . Sebelum melakukan penyerangan, kebanyakan hacker melakukan teknik <strong><em>Information Gathering</em></strong>, sebelum melakukan <em><strong>Vulnerability Scanning</strong></em> dan menanam <em><strong>exploit</strong></em>, beberapa diantaranya dia menanam <em><strong>Persistent Backdoors</strong></em> seperti <strong>xaishell.php</strong> untuk memaintain akses dia pada sistem korban. So, waspadalah, waspadalah. 😀
</p>
