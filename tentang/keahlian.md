---
id: 34
title: Keahlian Soft / Hard Skill
date: 2015-12-08T08:08:13+00:00
author: Eko Junaidi Salam
layout: page
guid: http://ekojunaidisalam.com/?page_id=34
dsq_thread_id:
  - "4387224336"
dsq_needs_sync:
  - "1"
---
<div style="text-align: center;"><img src="{{site.baseurl}}/wp-content/uploads/2015/12/skill-300x172.png" alt="Keahlian Soft Skill" /></div>
<h2 style="text-align: center;">Keahlian Soft Skill / Hard Skill</h2>

<p style="text-align: justify;">
  Sejak masih sekolah maupun saat kuliah saya telah sedikit demi sedikit melatih keahlian <em><strong>Soft Skill</strong></em> maupun <em><strong>Hard Skill</strong></em> saya dalam berorganisasi maupun dalam hal akademik. Saya percaya bahwa dengan mengasah keahlian ini saya dapat berbaur dengan berbagai macam tingkatan masyarakat.
</p>

<div style="text-align: center;">
  <h2>Pengalaman Organisasi</h2>
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
</div>
<br />
<p style="text-align: justify;">
  Keahlian <em><strong>Hard Skill</strong></em> saya juga lumayan, dengan sedikit melihat penyelesaian masalah pada situs <a href="https://stackoverflow.com/users/2735482/eko-junaidi-salam?tab=tags" target="_blank"><em><strong>Stackoverflow</strong></em></a>. Pada link itu teman &#8211; teman pembaca dapat melihat dengan jelas ada sekitar <strong>129</strong> <em><strong>Tags</strong> </em>kategori / label / keyword yang telah saya ikuti dengan total <a href="https://stackoverflow.com/users/2735482/eko-junaidi-salam?tab=answers&sort=votes" target="_blank"><strong>112 <em>Answers</em></strong></a>.
</p>

<p style="text-align: justify;">
  Dapat dilihat juga dari prestasi yang telah saya catatkan pada tabel dibawah ini :
</p>
<br />
<div style="text-align: center;">
  <h2>Prestasi</h2>
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
</div>
<br />
<p style="text-align: justify;">
  Sumber gambar : <a href="http://www.mitalent.org/elearning-soft-skills-program/" target="_blank">http://www.mitalent.org/elearning-soft-skills-program/</a>
</p>
