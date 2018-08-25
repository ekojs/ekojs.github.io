---
id: 38
title: Ringkasan Curriculum Vitae
date: 2015-12-08T08:55:13+00:00
author: Eko Junaidi Salam
layout: page
guid: http://ekojunaidisalam.com/?page_id=38
dsq_thread_id:
  - "4389236904"
image: /wp-content/uploads/2015/12/cropped-Ekojs-512x288.jpg
---
<div style="text-align: center;"><img src="{{site.baseurl}}/wp-content/uploads/2015/12/cropped-Ekojs-150x150.jpg" alt="Ringkasan" /></div>

<p style="text-align: justify;">
  Pada halaman ini, saya sertakan semua ringkasan <strong>Biodata</strong>, <strong>Pendidikan</strong> Formal, <strong>Seminar</strong>, <strong>Pelatihan</strong>, Pengalaman <strong>Organisasi</strong>, <strong>Prestasi</strong>, <strong>Kegiatan</strong> yang dilakukan, <strong>Pengalaman</strong> Kerja serta <strong>Keahlian</strong> yang dimiliki. Berikut dibawah ini adalah ringkasannya :
</p>

## Ringkasan Biodata

<table style="text-align: justify;">
	<tr>
		<td>Nama</td>
		<td>:</td>
		<td>{{site.data.biodataku.nama}}</td>
	</tr>
	<tr>
		<td>Tempat &amp; Tanggal Lahir</td>
		<td>:</td>
		<td>{{site.data.biodataku.ttl}}</td>
	</tr>
	<tr>
		<td>Jenis Kelamin</td>
		<td>:</td>
		<td>{{site.data.biodataku.sex}}</td>
	</tr>
	<tr>
		<td>Tinggi Badan</td>
		<td>:</td>
		<td>{{site.data.biodataku.tinggi}}</td>
	</tr>
	<tr>
		<td>Berat Badan</td>
		<td>:</td>
		<td>{{site.data.biodataku.berat}}</td>
	</tr>
	<tr>
		<td>Agama</td>
		<td>:</td>
		<td>{{site.data.biodataku.agama}}</td>
	</tr>
	<tr>
		<td>Status</td>
		<td>:</td>
		<td>{{site.data.biodataku.status}}</td>
	</tr>
	<tr>
		<td>Kewarganegaraan</td>
		<td>:</td>
		<td>{{site.data.biodataku.warga}}</td>
	</tr>
	<tr>
		<td>Alamat</td>
		<td>:</td>
		<td>{{site.data.biodataku.alamat}}</td>
	</tr>
	<tr>
		<td>Telepon</td>
		<td>:</td>
		<td>{{site.data.biodataku.telp}}</td>
	</tr>
	<tr>
		<td>E-mail</td>
		<td>:</td>
		<td>
		<u>
			<a href="mailto:{{site.data.biodataku.email}}">{{site.data.biodataku.email}}</a>
		</u>..:: 
		<a href="{{site.baseurl}}/tentang/kontak.html" target="_blank" rel="noopener noreferrer">Detil
		Kontak</a> ::..</td>
	</tr>
</table>

## Ringkasan Pendidikan Formal

<table style="text-align: justify; height: 323px;" width="607">
	<tr>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Sekolah / Kuliah</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Bidang</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Tingkat</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Tempat</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Periode</strong>
		</td>
	</tr>
	{% for p in site.data.pendidikanku %}
		<tr>
			<td style="text-align: left;">{{p.sekolah}}</td>
			<td style="text-align: center;">{{p.bidang}}</td>
			<td style="text-align: center;">{{p.tingkat}}</td>
			<td style="text-align: center;">{{p.tempat}}</td>
			<td style="text-align: center;">{{p.periode}}</td>
		</tr>
	{% endfor %}
</table>

## Ringkasan Seminar

<table style="text-align: justify;">
	<tr>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>No.</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Tahun</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Seminar</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Penyelenggara</strong>
		</td>
	</tr>
  
	{% for p in site.data.seminarku %}
		<tr>
			<td style="text-align: center;">{{forloop.index}}</td>
			<td style="text-align: center;">{{p.tahun}}</td>
			<td>{{p.seminar}}</td>
			<td style="text-align: center;">{{p.penyelenggara}}</td>
		</tr>
	{% endfor %}
</table>

## Ringkasan Pelatihan

<table style="text-align: justify;">
	<tr>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>No.</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Tahun</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Pelatihan</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Penyelenggara</strong>
		</td>
	</tr>
	{% for p in site.data.pelatihanku %}
		<tr>
			<td style="text-align: center;">{{forloop.index}}</td>
			<td style="text-align: center;">{{p.tahun}}</td>
			<td>{{p.pelatihan}}</td>
			<td style="text-align: center;">{{p.penyelenggara}}</td>
		</tr>
	{% endfor %}
</table>

## Ringkasan Pengalaman Organisasi

<table style="text-align: justify;">
	<tr>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>No.</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Tahun</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Organisasi</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Posisi</strong>
		</td>
	</tr>
	{% for p in site.data.organisasiku %}
		<tr>
			<td style="text-align: center;">{{forloop.index}}</td>
			<td style="text-align: center;">{{p.periode}}</td>
			<td>{{p.organisasi}}</td>
			<td style="text-align: center;">{{p.posisi}}</td>
		</tr>
	{% endfor %}
</table>

## Ringkasan Prestasi

<table style="text-align: justify;">
	<tr>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>No.</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Tahun</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Capaian</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Penyelenggara</strong>
		</td>
	</tr>
	{% for p in site.data.prestasiku %}
		<tr>
			<td style="text-align: center;">{{forloop.index}}</td>
			<td style="text-align: center;">{{p.tahun}}</td>
			<td>{{p.capaian}}</td>
			<td style="text-align: center;">{{p.penyelenggara}}</td>
		</tr>
	{% endfor %}
</table>

## Ringkasan Kegiatan

<table style="text-align: justify;">
	<tr>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>No.</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Tahun</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Kegiatan</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Posisi</strong>
		</td>
	</tr>
	{% for p in site.data.kegiatanku %}
		<tr>
			<td style="text-align: center;">{{forloop.index}}</td>
			<td style="text-align: center;">{{p.tahun}}</td>
			<td>{{p.kegiatan}}</td>
			<td style="text-align: center;">{{p.posisi}}</td>
		</tr>
	{% endfor %}
</table>

## Ringkasan Pengalaman Kerja

<table style="text-align: justify;">
	<tr>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>No.</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Tempat</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Bisnis</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Posisi</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Periode</strong>
		</td>
	</tr>
	{% for p in site.data.pengalamanku %}
		<tr>
			<td style="text-align: center;">{{forloop.index}}</td>
			<td>{{p.tempat}}</td>
			<td>{{p.bisnis}}</td>
			<td style="text-align: center;">{{p.posisi}}</td>
			<td style="text-align: center;">{{p.periode}}</td>
		</tr>
	{% endfor %}
</table>

## Ringkasan Keahlian

<table style="text-align: justify;">
	<tr>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>No.</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Keahlian</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Pengalaman</strong>
		</td>
		<td style="text-align: center; width: &#39;100px&#39;;">
			<strong>Tingkat</strong>
		</td>
	</tr>
	{% for p in site.data.keahlianku %}
		<tr>
			<td style="text-align: center;">{{forloop.index}}</td>
			<td>{{p.keahlian}}</td>
			<td>{{p.pengalaman}}</td>
			<td style="text-align: center;">{{p.tingkat}}</td>
		</tr>
	{% endfor %}
</table>
