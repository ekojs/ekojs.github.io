---
id: 243
title: Membuat Certificate menggunakan XAMPP pada Windows 7
date: 2016-06-02T12:29:42+00:00
author: Eko Junaidi Salam
layout: post
guid: http://ekojunaidisalam.com/?p=243
permalink: /2016/06/02/membuat-certificate/
dsq_thread_id:
  - "4876890529"
categories:
  - Artikel
  - Teknologi
  - 'Tip &amp; Trik'
tags:
  - certificate
  - https
  - ssl
  - xampp
---
<div style="text-align: center;"><img src="https://ekojunaidisalam.com/wp-content/uploads/2016/06/digital-certificates.jpg" alt="Membuat Certificate" /></div>
<h2 style="text-align: center;">Membuat Certificate dengan OpenSSL XAMPP</h2>

<div style="text-align: justify;">
  Hallo teman &#8211; teman pembaca, ketemu kembali dalam artikel Membuat Certificate menggunakan xampp pada windows 7 ini setelah beberapa lama tiada update. 😀
</div>

<div style="text-align: justify;">
</div>

<div style="text-align: justify;">
  Topik kali ini saya akan membahas bagaimana membuat sebuah <i>certificate </i>menggunakan openssl pada xampp. Karena saya menggunakan windows 7 maka topik saya khususkan untuk windows 7.
</div>

<div style="text-align: justify;">
</div>

<div style="text-align: justify;">
  Tool yang kita butuhkan kali ini adalah :
</div>

  1. xampp tentunya, lokasi saya ada di : <code>C:\xampp\</code>

  2. openssl pada <code>C:\xampp\apache\bin</code>

  3. Powershell pada windows 7

<p style="text-align: justify;">
  Oke, kita langsung saja tak perlu banyak acara. Lakukan langkah dibawah ini secara berurutan :<a name='more'></a>
</p>

```
1. cd c:\xampp\apache\bin  
2. openssl genrsa -des3 -out O:\Titip\ekojs_2048.key 2048  
      Masukkan passphrase untuk key anda  
# Ekstrak private key tanpa passphrase, dan backup file asli  
3. cp O:\Titip\ekojs_2048.key O:\Titip\ekojs_2048.key.secure  
4. openssl rsa -in O:\Titip\ekojs_2048.key.secure -out O:\Titip\ekojs_2048.key  
5. openssl req -new -key O:\Titip\ekojs_2048.key.secure -out O:\Titip\ekojs_2048.csr -config C:\xampp\apache\conf\openssl.cnf  
6. openssl x509 -req -days 365 -in O:\Titip\ekojs_2048.csr -signkey O:\Titip\ekojs_2048.key -out O:\Titip\ekojs_2048.crt  
7. Certificate anda siap digunakan 😀  
```

Bila ada pesan:

<code>WARNING: can't open config file: /usr/local/ssl/openssl.cnf</code>

<p style="text-align: justify;">
  temen-temen bisa mengabaikannya selama tidak menghentikan proses generate filenya.
</p>

<p style="text-align: justify;">
  Informasi Tambahan : bila <i>certificate </i>yang dibuat nantinya akan digunakan pada salah satu website yang teman pembaca miliki maka saat membuat *.csr pada bagian <i><b>Common Name / FQDN</b></i> harus di isi sesuai alamat webnya misal : <b>www.example.com</b> atau <b>webapp.localku</b> dan sejenisnya.
</p>

<p style="text-align: justify;">
  Bila ada permasalahan, pertanyaan, keluhan, uneg-uneg dan kriteria uneg-uneg lainnya, silahkan <i>comment </i>ya&#8230;.<br /> Terima kasih&#8230;.
</p>

Sumber Artikel : http://eko-artikel.blogspot.co.id/2015/07/cara-membuat-certificate.html
  
Sumber Gambar : http://securityaffairs.co/wordpress/wp-content/uploads/2013/12/digital-certificates.jpg
