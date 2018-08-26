---
layout: post
title: Integrating CodeIgniter 3 with Laravel-Mix
author: Eko Junaidi Salam
date: 2018-08-25T21:26:56+00:00
permalink: /2018/08/25/integrate-ci3-with-laravel-mix/
categories:
  - Programming
  - Artikel
  - Teknologi
tags:
  - CodeIgniter
  - Laravel-Mix
  - Framework
  - PHP
  - NPM
  - Nodejs
---
<h2 style="text-align: center;">
  <img src="{{site.baseurl}}/assets/img/ci3.png" width="20%" height="20%" />
  <img src="{{site.baseurl}}/assets/img/logo-mix.svg" /><br />
  CodeIgniter 3 with Laravel-Mix
</h2>
<p style="text-align: justify;">
Pada kesempatan kali ini saya ingin mengulas tentang integrasi framework CodeIgniter 3 dengan Laravel-Mix. Mungkin sudah lama sekali sepertinya dari postingan terakhir di website ini, tapi alhamdulillah bisa menulis kembali saat ini. Artikel ini dibuat karena beberapa hari ini penulis sedang melakukan <i>refactoring</i> seluruh assets pada beberapa aplikasi web. Jadi butuh tools untuk mempermudah kompilasi atau bundling beberapa file js, scss dan gambar menjadi satu kesatuan assets.
</p>
<p style="text-align: justify;">
Sebenarnya banyak teknologi yang bisa digunakan untuk melakukan tugas kompilasi atau bundling ini, seperti halnya <code>grunt</code>, <code>gulp</code>, dan <code>webpack</code> yang umum digunakan sebagai <i>Task Runners</i> untuk menjalankan tugas kompilasi. Namun dibalik teknologi itu semua sebenarnya bergantung dari kebutuhan kita sendiri lebih <i>prefer</i> menggunakan yang mana, karena saya percaya semua teknologi itu ada untuk saling melengkapi serta mempermudah pekerjaan kita.</p><a name='more'></a>
<p style="text-align: justify;">Nah kenapa akhirnya teknologi yang saya gunakan menggunakan <b>CodeIgniter 3</b> dan <b>Laravel-Mix</b> ? tentu karena menurut hemat saya menggunakan codeigniter lebih mudah dan sourcenya pun sangat kecil sekitar `~2MB` sedangkan laravel-mix lebih memudahkan dalam melakukan kompilasi dan bundling berbagai jenis stylesheet dan javascript juga hal yang utama karena laravel-mix itu sendiri menggunakan teknologi <code>webpack</code> dalam melakukan tugasnya. Banyak artikel yang telah membahas perbandingan beberapa teknologi tersebut salah satunya dari artikel <a href="https://blog.vanila.io/webpack-what-is-it-and-is-it-better-than-gulp-375db8011d22" target="_blank">blog.vanila.io</a> ini.
</p>
<p style="text-align: justify;">
Oke, agar tidak terlalu panjang ceritanya. Kita langsung praktek melakukan integrasi antara CodeIgniter 3 dengan Laravel-Mix. Sebagai pengingat, segala kerusakan/kegagalan yang ditimbulkan oleh karena mengikuti petunjuk dibawah ini <b>BUKAN</b> tanggung jawab penulis. 
</p>

#### Persiapan
1. Silahkan <i>clone</i> dan <i>star</i> repo <a href="https://github.com/ekojs/ci3-with-laravel-mix"><span class="icon icon--github">{% include icon-github.svg %}</span><span class="username">ci3-with-laravel-mix</span></a>.
2. Bila anda tak memiliki akun github gunakan clone HTTPS [berikut](https://github.com/ekojs/ci3-with-laravel-mix.git) (<i>Jaman gini belum punya akun bro/sist ? bikin lah [kesini](https://github.com/join?source=header-home)</i>).
3. Sesuaikan Operating System yang digunakan, Repo ini telah diuji menggunakan *nix OS dan Windows OS. Pastikan anda telah memiliki git dan dapat mengaksesnya dari tools kesayangan anda, untuk pengguna windows jangan lupa untuk menyertakan lokasi binary pada `System Path`. Silahkan baca [instalasi git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) bila belum memiliki git. 
4. Buka console anda, untuk windows gunakan `powershell` anda. Lalu kemudian ketik perintah berikut ini, pastikan anda berada dilokasi `root folder` pada web server anda silahkan gunakan `XAMPP`, `Nginx`, `Docker` atau apapun terserah anda.

```bash
#Bila menggunakan ssh link
git clone git@github.com:ekojs/ci3-with-laravel-mix.git

#Bila menggunakan https link bagi yg belum memiliki akun git
git clone https://github.com/ekojs/ci3-with-laravel-mix.git
```

#### Instalasi
1. Setelah berhasil di clone pada komputer lokal anda, silahkan masuk kedalam folder `ci3-with-laravel-mix`.
```bash
cd ci3-with-laravel-mix
```
2. Kemudian silahkan install `npm modules` yang ada pada `package.json` tersebut dengan perintah berikut, bila berhasil maka akan muncul folder bernama `node_modules`.
```bash
npm install
```
3. Setup symlink untuk module `cross-env` pada lingkungan path anda. Untuk pengguna *unix jalankan perintah berikut, silahkan sesuaikan lokasi folder anda. Untuk pengguna Windows install `cross-env` secara global kemudian masukkan ke dalam `Environtment System Path` Windows anda, biasanya ada pada lokasi `C:\Users\users\AppData\Roaming\npm` sesuaikan dengan lokasi folder anda. Pastikan `cross-env` ada pada daftar tersebut.

```bash
#*unix
sudo ln -s /home/users/ci3-mix/node_modules/cross-env/dist/bin/cross-env.js /usr/local/bin/cross-env
#Windows
npm install -g cross-env
npm -g list --depth=0
```

#### Konfigurasi
1. Perhatikan 2 lokasi penting seperti folder `src` dan `assets` serta beberapa file seperti `package.json` dan `webpack.mix.js`.
<img src="{{site.baseurl}}/assets/img/lokasi_penting1.png" />
<img src="{{site.baseurl}}/assets/img/lokasi_penting2.png" />
2. Konten file `package.json`, berisi _dependency development_ yang diperlukan dalam menjalankan laravel-mix.
<script src="http://gist-it.appspot.com/https://github.com/ekojs/ci3-with-laravel-mix/blob/master/package.json"></script>
3. Konten file `webpack.mix.js`, berisi tugas yang akan dilakukan bila terdapat perubahan pada file _javascript_ dan _stylesheet_ pada folder `src/`.

```bash
let mix = require('laravel-mix');
// mix.setPublicPath('./'); // Uncomment this if you use windows environment, don't forget to set your npm global binary location into your Environment System Path.
mix.js('src/js/app.js', 'assets/js')
    .sass('src/css/app.scss', 'assets/css')
    .copyDirectory('src/img', 'assets/img')
    .options({
        fileLoaderDirs: { // To load fonts into assets folder
            fonts: 'assets/fonts'
        }
    });
    /**
     * If you want to separate your javascript from main javascript app.js you can use combine to combine multiple javascript into another file. Please reorder as your need.
     */
    // .combine([
    //    'node_modules/admin-lte/bower_components/bootstrap-datepicker/dist/js/bootstrap-datepicker.min.js',
    //     'node_modules/admin-lte/plugins/bootstrap-wysihtml5/bootstrap3-wysihtml5.all.min.js'
    // ], 'assets/js/vendor.js');
```

<p style="text-align: justify;">
File <code>package.json</code> berisi <i>dependency module</i> yang digunakan dalam repo ini, seperti <code>bootstrap-sass</code> digunakan untuk stylesheet frontend menggunakan bootstrap 3, <code>cross-env</code> digunakan untuk mengatur lingkungan development, <code>jquery</code> digunakan untuk menjalankan external library javascript dan <code>laravel-mix</code> digunakan untuk melakukan kompilasi dan bundling terhadap object stylesheet dan javascript tersebut.</p>
<p style="text-align: justify;">
Kemudian selanjutnya folder <code>src/</code> berisi konten yang akan dikompilasi dan dibundle. Secara spesifik file pada <code>src/js/app.js</code> dan <code>src/css/app.scss</code> tersebutlah yang akan dieksekusi bila terdapat perubahan, kemudian hasil dari eksekusi tersebut ada pada folder <code>assets/</code></p>
<p style="text-align: justify;">
Sesuaikan konfigurasi pada file <code>webpack.mix.js</code>, misal bila anda pengguna windows maka <i>uncomment</i> script <code>mix.setPublicPath('./');</code>. Bila menginginkan library javascript external digabung namun di pisah dari main file <code>app.js</code> maka gunakan script <code>mix.combine(files, destination);</code> seperti yang dicontohkan pada baris yang dikomentar pada file <code>webpack.mix.js</code></p>

#### Test It

<p style="text-align: justify;">
Bila seluruh konfigurasi telah dilakukan dan tidak ada error, maka silahkan test dengan menjalankan perintah dibawah ini. Kemudian buka browser anda untuk melihat hasilnya</p>
```bash
#Untuk development
npm run watch-poll

#Untuk production
npm run prod
```

<p style="text-align: justify;">Berikut screenshot tampilannya</p>
<img src="{{site.baseurl}}/assets/img/welcome.png" />
<p style="text-align: center;">Ini adalah tampilan welcome message default dari CodeIgniter.</p>
<img src="{{site.baseurl}}/assets/img/msgbox.png" />
<p style="text-align: center;">Ini adalah tampilan message box yang berasal dari hasil kompilasi dan bundling pada file scss dan js difolder <code>src/</code>.</p>

<p style="text-align: justify;">
Horeee... anda telah melakukan integrasi CodeIgniter 3 dengan Laravel-Mix.</p>

<p style="text-align: justify;">Bila ada pertanyaan, kebingungan coding di github, keluhan, kritik, atau pun saran yang membangun silahkan komentar disini. Untuk mencoba menjalankan aplikasi di github, jangan lupa untuk membaca <code><a href="https://github.com/ekojs/ci3-with-laravel-mix/blob/master/README.md" target="_blank">README.md</a></code> agar tidak kebingungan atau bahkan error. ^^ </p>