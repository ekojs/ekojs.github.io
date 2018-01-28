---
id: 217
title: Generator CRUD menggunakan Integrasi CI dan ExtJS4.2
date: 2016-04-06T07:24:19+00:00
author: Eko Junaidi Salam
layout: post
guid: https://ekojunaidisalam.com/?p=217
permalink: /2016/04/06/integrasi-ci-dan-extjs4-2/
dsq_thread_id:
  - "4723442501"
dsq_needs_sync:
  - "1"
categories:
  - Artikel
  - Programming
  - Teknologi
  - 'Tip &amp; Trik'
tags:
  - 'CI &amp; ExtJS'
  - Code Igniter
  - extjs
  - framework
  - generator
  - github
  - integrate
  - javascript
  - php
  - web desktop
---
<div style="text-align: center;">
  <img src="https://ekojunaidisalam.com/wp-content/uploads/2016/04/Generator-CI_ExtJS.png" alt="Integrasi CI dan ExtJS4.2" />
</div>
<h2 style="text-align: center;">Integrasi CI dan ExtJS4.2</h2>

<p style="text-align: justify;">
  Artikel sebelumnya telah membahas tentang <a href="https://ekojunaidisalam.com/2016/03/04/integrate-extjs4-2-with-nodejs/" target="_blank">Integrasi ExtJS & NodeJS</a> kali ini saya akan membahas Integrasi CI dan ExtJS4.2. <em><strong>CodeIgniter (CI)</strong></em> adalah <em>framework</em> yang menggunakan model MVC dimana bahasa pemrograman yang digunakan adalah bahasa PHP, Sedangkan <em><strong>ExtJS</strong></em> adalah <em>Framework</em> yang menggunakan model MVC juga namun bahasa yang digunakan adalah Javascript. Dengan memanfaatkan model MVC tersebut itulah integrasi ini dilakukan, bila ExtJS menangani user di bagian <em><strong>FrontEnd</strong></em> maka nantinya CI lah yang akan menangani bagian <em><strong>BackEnd</strong></em> nya.
</p>

<p style="text-align: justify;">
  Mari kita perhatikan struktur model MVC pada keduanya, struktur hasil integrasi keduanya bisa berbeda bergantung logic yang dipergunakan ketika menggabungkan kedua framework tersebut. Disini saya akan mencontohkan struktur yang sederhana dalam integrasi keduanya.
</p>

<pre class="lang:default decode:true" title="Struktur MVC pada ExtJS dan CodeIgniter">Struktur pada ExtJS, secara sederhana :
ExtJS
|______ app
|	|___ controller
|	|	|___ Main.js
|	|___ model
|	|___ store
|	|___ view
|	|	|__ Main.js
|	|	|__ Navigation.js
|	|	|__ Viewport.js
|	|__ Application.js
|______ ext


Struktur pada CI, secara sederhana :

CI
|__ application
|	|__ controllers
|	|	|__ welcome.php
|	|__ models
|	|__ libraries
|	|__ third_party
|	|__ views
|		|__ welcome_message.php
|__ system
|__ index.php

Struktur hasil Integrasi ketika di deploy :

CI & ExtJS4.2
|__ application
|	|__ controllers
|	|	|__ welcome.php
|	|__ models
|	|__ libraries
|	|__ third_party
|	|__ views
|		|__ welcome_message.php
|__ system
|__ resources
|__ index.php
|__ app.js</pre>

<p style="text-align: justify;">
  <a name='more'></a>Setelah kita mengetahui struktur dari masing &#8211; masing framework, mari kita mulai membuat kostumisasi pada keduanya. Pertama kita lakukan konfigurasi pada file 
  
  <em><a href="https://github.com/ekojs/ci_extjs/blob/master/application/config/config.php" target="_blank">config.php</a> </em>untuk memastikan url pada CI tidak menampilkan <em>index.php</em>, <em><a href="https://github.com/ekojs/ci_extjs/blob/master/application/config/database.php" target="_blank">database.php</a> </em>untuk memastikan konfigurasi & koneksi ke database karena faktor utama dari generator ini adalah <a href="https://github.com/ekojs/ci_extjs/blob/master/resources/test.sql" target="_blank"><strong>Database</strong> </a>begitu juga perlu di perhatikan bahwa setiap tabel harus memiliki minimal 1 <em>Primary Key</em>, dan <em><a href="https://github.com/ekojs/ci_extjs/blob/master/application/config/routes.php" target="_blank">route.php</a> </em>untuk memastikan controller utama yang akan dijalankan ketika base_url diketikkan.
</p>

<p style="text-align: justify;">
  Setelah konfigurasi CI selesai, kemudian kita melangkah untuk konfigurasi pada ExtJS. File yang sangat berpengaruh disini adalah file di dalam folder <em><strong>store</strong></em>, contoh file <a href="https://github.com/ekojs/ci_extjs/blob/master/app/store/s_pengarang.js" target="_blank">store</a> seperti dibawah ini :
</p>

<pre class="lang:default decode:true " title="Contoh file store">/**
 * Class	: CSE_pengarang
 * 
 * Table	: pengarang
 *  
 * @author Eko Junaidi Salam
 *
 */
 Ext.define('EJS.store.s_pengarang', {
	extend	: 'Ext.data.Store',
	alias	: 'widget.pengarangStore',
	model	: 'EJS.model.m_pengarang',
	
	autoLoad	: false,
	autoSync	: false,
	
	storeId		: 'pengarang',
	
	pageSize	: 15, // number display per Grid
	
	proxy: {
		type: 'ajax',
		api: {
			read    : 'c_pengarang/getAll',
			create	: 'c_pengarang/save',
			update	: 'c_pengarang/save',
			destroy	: 'c_pengarang/delete'
		},
		actionMethods: {
			read    : 'POST',
			create	: 'POST',
			update	: 'POST',
			destroy	: 'POST'
		},
		reader: {
			type            : 'json',
			root            : 'data',
			rootProperty    : 'data',
			successProperty : 'success',
			messageProperty : 'message'
		},
		writer: {
			type            : 'json',
			writeAllFields  : true,
			root            : 'data',
			encode          : true
		},
		listeners: {
			exception: function(proxy, response, operation){
				Ext.MessageBox.show({
					title: 'REMOTE EXCEPTION',
					msg: operation.getError(),
					icon: Ext.MessageBox.ERROR,
					buttons: Ext.Msg.OK
				});
			}
		}
	},
	
	constructor: function(){
		this.callParent(arguments);
	}
	
});</pre>

<p style="text-align: justify;">
  Coba perhatikan konfigurasi pada proxy, proses crud semua menggunakan pola pada CI dalam arti kata proses backend dilakukan oleh CI. Begitu pula bila proses remote filter diaktifkan, namun pada contoh disini tidak saya aktifkan.
</p>

<p style="text-align: justify;">
  Setelah konfigurasi diatas dilakukan barulah menyesuaikan pada konfigurasi tambahan seperti penambahan <em>library <strong><a href="https://github.com/ekojs/ci_extjs/blob/master/application/libraries/egen.php" target="_blank">egen.php</a></strong></em> serta modul <em><a href="https://github.com/ekojs/ci_extjs/tree/master/application/third_party" target="_blank">third party</a></em> lainnya seperti PHPExcel, dll. Semua konfigurasi dapat dilihat secara detail pada <a href="https://github.com/ekojs/ci_extjs" target="_blank">Github </a>tersebut. Bila konfigurasi telah berhasil dilakukan maka hasil generator dapat dilihat seperti gambar dibawah ini. Konfigurasi default untuk mengakses generator ada pada alamat <a href="http://localhost/ci_extjs/welcome/gce" target="_blank">http://localhost/ci_extjs/welcome/gce</a>.
</p>

<p style="text-align: justify;">
  <a href="https://ekojunaidisalam.com/wp-content/uploads/2016/04/Hasil.png" rel="attachment wp-att-221"><img class="aligncenter wp-image-221 size-full" src="https://ekojunaidisalam.com/wp-content/uploads/2016/04/Hasil.png" alt="Hasil Generator CI & ExtJS" width="1535" height="876" srcset="https://ekojunaidisalam.com/wp-content/uploads/2016/04/Hasil.png 1535w, https://ekojunaidisalam.com/wp-content/uploads/2016/04/Hasil-300x171.png 300w, https://ekojunaidisalam.com/wp-content/uploads/2016/04/Hasil-768x438.png 768w, https://ekojunaidisalam.com/wp-content/uploads/2016/04/Hasil-1024x584.png 1024w, https://ekojunaidisalam.com/wp-content/uploads/2016/04/Hasil-500x285.png 500w" sizes="(max-width: 1535px) 100vw, 1535px" /></a>Contoh Konfigurasi file view pada <span class="lang:default decode:true crayon-inline "><a href="https://github.com/ekojs/ci_extjs/blob/master/application/views/welcome.php" target="_blank">C:\xampp\htdocs\ci_extjs\application\views\welcome.php</a></span>
</p>

<pre class="lang:default decode:true " title="Contoh integrasi CI & ExtJS pada view">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
	&lt;meta charset="utf-8"&gt;
	&lt;title&gt;Welcome to Generator CI dan ExtJS4.2&lt;/title&gt;

	&lt;meta name="author" content="Eko Junaidi Salam"&gt;
	&lt;meta name="email" content="eko_junaidisalam@live.com"&gt;
	&lt;meta name="description" content="Integrasi CI dan ExtJS4.2"&gt;
	&lt;meta name="keywords" content="ERP"&gt;

	&lt;script type="text/javascript"&gt;
		var base_url = '&lt;?php echo base_url();?&gt;';
	&lt;/script&gt;
	&lt;!-- &lt;x-compile&gt; --&gt;
        &lt;!-- &lt;x-bootstrap&gt; --&gt;
			&lt;link rel="stylesheet" href="&lt;?php echo base_url();?&gt;resources/css/icons.css"/&gt;
            &lt;link rel="stylesheet" href="bootstrap.css"&gt;
            &lt;script src="&lt;?php echo base_url();?&gt;ext/ext-dev.js"&gt;&lt;/script&gt;
            &lt;script src="&lt;?php echo base_url();?&gt;bootstrap.js"&gt;&lt;/script&gt;
        &lt;!-- &lt;/x-bootstrap&gt; --&gt;
        &lt;script type="text/javascript" src="&lt;?php echo base_url();?&gt;app.js"&gt;&lt;/script&gt;
    &lt;!-- &lt;/x-compile&gt; --&gt;
	
&lt;/head&gt;
&lt;body&gt;
&lt;div id="loading-mask" style=""&gt;&lt;/div&gt;
    &lt;div id="loading"&gt;
        &lt;div class="loading-indicator"&gt;
            &lt;img src="&lt;?php echo base_url();?&gt;resources/images/loading.gif" style="margin-right:8px;float:left;vertical-align:top;"/&gt;
        &lt;/div&gt;
    &lt;/div&gt;
    
    &lt;script type="text/javascript"&gt;
    Ext.onReady(function() {

        (Ext.defer(function() {
            var hideMask = function () {
                Ext.get('loading').remove();
                Ext.fly('loading-mask').animate({
                    opacity:0,
                    remove:true
                });
            };

            Ext.defer(hideMask, 250);

        },500));
    });
    &lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>

<p style="text-align: justify;">
  Repo <strong>Struktur hasil Integrasi CI dan ExtJS4.2</strong> dapat dilihat pada branch <a href="https://github.com/ekojs/ci_extjs/tree/deploy" target="_blank">deploy</a>. Contoh halaman bila berhasil dijalankan bisa dilihat pada <a href="http://ekojs.github.io/ci_extjs" target="_blank">http://ekojs.github.io/ci_extjs</a> atau contoh hasil deploy bisa dilihat di <a href="http://ekojs.github.io/akreditasi" target="_blank">http://ekojs.github.io/akreditasi</a>. Karena pages pada githbu.io adalah halaman non PHP maka pada contoh diatas saya menghilangkan seluruh aksi PHP dan saya buat secara statik untuk &#8220;menggambarkan&#8221; hasil akhir bila ExtJS di deploy.
</p>

<p style="text-align: justify;">
  Bila ada pertanyaan, kebingungan coding di <a href="https://github.com/ekojs/ci_extjs" target="_blank">github</a>, keluhan, kritik, atau pun saran yang membangun silahkan komentar disini atau di github.
</p>
