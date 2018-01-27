---
id: 344
title: Penerapan K-Means Clustering pada Multivariate Data
date: 2017-02-14T02:02:49+00:00
author: Eko Junaidi Salam
layout: post
guid: http://ekojunaidisalam.com/?p=344
permalink: /2017/02/14/k-means-pada-multivariate-data/
dsq_thread_id:
  - "5548480900"
dsq_needs_sync:
  - "1"
categories:
  - Algorithm
  - Artikel
  - Data Science
  - Teknologi
tags:
  - Data Mining
  - Data Science
  - K-Means Algorithm
  - K-Means Clustering
  - Multivariate Data
---
<h2 style="text-align: center;">
  <a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/k-means_result.png"><img class="aligncenter size-full wp-image-340" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/k-means_result.png" alt="Multivariate Data" width="961" height="988" srcset="https://ekojunaidisalam.com/wp-content/uploads/2017/02/k-means_result.png 961w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/k-means_result-292x300.png 292w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/k-means_result-768x790.png 768w" sizes="(max-width: 961px) 100vw, 961px" /></a>Penerapan K-Means Clustering pada Multivariate Data
</h2>

<p style="text-align: justify;">
  Tidak sedikit yang menanyakan tentang penerapan K-Means, beberapa menanyakan apakah K-Means dapat digunakan pada Multivariate Data ? beberapa diantaranya juga menanyakan apakah bisa digunakan pada data dengan attribut yang banyak ? ada juga yang menanyakan apakah bisa untuk melakukan clustering terhadap data non numerik ? dan beberapa pertanyaan lainnya.
</p>

<p style="text-align: justify;">
  Pada artikel kali ini, khusus penulis akan membahas penerapan <em>K-Means Clustering</em> pada <em><strong>Multivariate Data</strong></em>. Apa itu multivariate data ? adalah data yang memiliki variasi tipe data yang berbeda. Data dapat kita bedakan berdasarkan tipenya, seperti :
</p>

<li style="text-align: justify;">
  <em><strong>Quantitative Data / Numerical Data</strong></em>, adalah data yang berupa data angka, baik integer, positive/negative integer, atau pun float/decimal.
</li>
<li style="text-align: justify;">
  <em><strong>Binary Data</strong></em>, adalah data yang hanya berisi data 0/1, true/false, ya/tidak, Pria/Wanita, dll.
</li>
<li style="text-align: justify;">
  <strong>Nominal Data</strong>, adalah data yang berisi pilihan, dimana data hanya dapat dipilih satu dari sekian banyak pilihan. Contoh : Dalam pertanyaan dengan pilihan ganda hanya boleh memilih 1 jawaban dari opsi (a, b, c, d), dsb.
</li>
<li style="text-align: justify;">
  <strong>Ordinal Scale</strong>, adalah data yang menyerupai skala atau jangkauan data, dimana data tersebut tidak ada nilai quatitative yang signifikan. Contoh : (Sangat Tidak Setuju, Tidak Setuju, Setuju, Sangat Setuju), atau (Memuaskan, Sangat Memuaskan, dan Dengan Pujian), dsb.
</li>

Setelah mengetahui tipe datanya, mari kita langsung ke pokok diskusi. Berikut dibawah ini adalah data sample yang saya miliki.<a name='more'></a>

<table width="623">
  <tr>
    <td style="text-align: center;" colspan="6" width="623">
      Sample Data
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      <strong>Nama</strong>
    </td>
    
    <td style="text-align: center;">
      <strong>IPK</strong>
    </td>
    
    <td style="text-align: center;">
      <strong>Semester</strong>
    </td>
    
    <td style="text-align: center;">
      <strong>Kampus</strong>
    </td>
    
    <td style="text-align: center;">
      <strong>Tingkat Kesulitan</strong>
    </td>
    
    <td style="text-align: center;">
      <strong>Kepuasan</strong>
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      A
    </td>
    
    <td style="text-align: center;">
      3.00
    </td>
    
    <td style="text-align: center;">
      7
    </td>
    
    <td style="text-align: center;">
      ITS
    </td>
    
    <td>
      Sangat Susah
    </td>
    
    <td>
      Puas
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      B
    </td>
    
    <td style="text-align: center;">
      3.50
    </td>
    
    <td style="text-align: center;">
      5
    </td>
    
    <td style="text-align: center;">
      ITB
    </td>
    
    <td>
      Susah
    </td>
    
    <td>
      Sangat Puas
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      C
    </td>
    
    <td style="text-align: center;">
      3.40
    </td>
    
    <td style="text-align: center;">
      3
    </td>
    
    <td style="text-align: center;">
      UGM
    </td>
    
    <td>
      Gampang
    </td>
    
    <td>
      Puas
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      D
    </td>
    
    <td style="text-align: center;">
      3.80
    </td>
    
    <td style="text-align: center;">
      6
    </td>
    
    <td style="text-align: center;">
      ITS
    </td>
    
    <td>
      Gampang
    </td>
    
    <td>
      Sangat Puas
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      E
    </td>
    
    <td style="text-align: center;">
      3.00
    </td>
    
    <td style="text-align: center;">
      7
    </td>
    
    <td style="text-align: center;">
      UI
    </td>
    
    <td>
      Sangat Susah
    </td>
    
    <td>
      Tidak Puas
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      F
    </td>
    
    <td style="text-align: center;">
      3.40
    </td>
    
    <td style="text-align: center;">
      5
    </td>
    
    <td style="text-align: center;">
      ITB
    </td>
    
    <td>
      Susah
    </td>
    
    <td>
      Puas
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  Akan dilakukan proses clustering berdasarkan data diatas menggunakan K-Means Clustering. Bagaimana caranya ? caranya adalah dengan melakukan <em><strong>normalisasi data</strong></em> terlebih dahulu. Bagaimana melakukannya ? mari kita ikuti step by step dibawah ini. Penulis juga menyertakan file excel yang diembed disini untuk mempermudah pemahaman teman-teman pembaca.
</p>

<p style="text-align: center;">
</p>

<p style="text-align: justify;">
  Mari kita kupas bersama &#8211; sama, mungkin teman &#8211; teman pembaca telah melihat sekilas tab <strong>Raw Data</strong>, dan <strong>Vector</strong>. Tapi mari kita ikut step by step dibawah ini.
</p>

<p style="text-align: justify;">
  Hal yang perlu kita lakukan adalah :
</p>

<li style="text-align: justify;">
  Mentransformasi data diatas menjadi data vector.
</li>
<li style="text-align: justify;">
  Data yang bukan numerik, dibuatkan dummy variabel bila diperlukan.
</li>
<li style="text-align: justify;">
  Melakukan normalisasi data dengan menghitung <em><strong>Distance Matrix</strong></em> pada setiap <em>attribute</em>.
</li>
<li style="text-align: justify;">
  Terapkan algoritma sesuai dengan data yang dimiliki, bisa menggunakan <a href="https://en.wikipedia.org/wiki/Euclidean_distance" target="_blank"><em><strong>Euclidean Distance</strong></em></a>, <a href="https://en.wikipedia.org/wiki/Hamming_distance" target="_blank"><em><strong>Hamming Distance</strong></em></a>, <a href="https://en.wikipedia.org/wiki/Taxicab_geometry" target="_blank"><em><strong>Manhattan Distance</strong></em></a>, <a href="https://en.wikipedia.org/wiki/Minkowski_distance" target="_blank"><em><strong>Minkowski Distance</strong></em></a>, <a href="https://en.wikipedia.org/wiki/Chebyshev_distance" target="_blank"><em><strong>Chebyshev Distance</strong></em></a>, ataupun algoritma lainnya untuk melakukan normalisasi silahkan riset sendiri 😀 .
</li>
<li style="text-align: justify;">
  Buat Aggregate Data.
</li>

<p style="text-align: justify;">
  Karena attribut (Kampus, Tingkat Kesulitan, dan Kepuasan) adalah data non numerik. Maka kita perlu membuat dummy variabel berdasarkan rumus : <a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/nominal_var.gif"><img class="aligncenter size-full wp-image-346" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/nominal_var.gif" alt="" width="84" height="48" /></a>dimana <a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/nominal_var1.gif"><img class="aligncenter size-full wp-image-347" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/nominal_var1.gif" alt="" width="23" height="27" /></a>adalah<em><strong> Ceiling Symbol</strong></em>, dimana hasilnya selalu dinaikkan ke nilai integer selanjutnya. Contoh : <span class="lang:default decode:true crayon-inline ">dv = 2.3</span>  , maka ceil <span class="lang:default decode:true crayon-inline ">dv = 3</span> , bila <span class="lang:default decode:true crayon-inline ">dv = 4.3</span> , maka ceil <span class="lang:default decode:true crayon-inline ">dv = 5</span> , dst. Sedangkan variabel <em><strong>c</strong></em> adalah adalah jumlah kategori dalam data. Contoh : Kampus (ITB, ITS, UGM, UI) ada 4 kategori maka <span class="lang:default decode:true crayon-inline ">c = 4</span> , dst.
</p>

<table style="border-collapse: collapse; width: 577px; height: 660px;" border="0" width="320" cellspacing="0" cellpadding="0">
  <colgroup> <col style="width: 48pt;" span="5" width="64" /> </colgroup> <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15pt; width: 240pt; text-align: center;" colspan="5" width="320" height="20">
      Transform Data To Vector
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
      Kampus
    </td>
    
    <td class="xl63">
      ITB
    </td>
    
    <td class="xl63">
      ITS
    </td>
    
    <td class="xl63">
      UGM
    </td>
    
    <td class="xl63">
      UI
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
      dv1
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
      1
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
      1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
      dv2
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
      1
    </td>
    
    <td class="xl63">
      1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl64">
      (0,0)
    </td>
    
    <td class="xl64">
      (1,0)
    </td>
    
    <td class="xl64">
      (0,1)
    </td>
    
    <td class="xl65">
      (1,1)
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
    </td>
  </tr>
  
  <tr style="height: 45.0pt;">
    <td class="xl66" style="height: 45.0pt; width: 48pt;" width="64" height="60">
      Tingkat Kesulitan
    </td>
    
    <td class="xl66" style="width: 48pt;" width="64">
      Sangat Susah
    </td>
    
    <td class="xl66" style="width: 48pt;" width="64">
      Susah
    </td>
    
    <td class="xl66" style="width: 48pt;" width="64">
      Gampang
    </td>
    
    <td class="xl66" style="width: 48pt;" width="64">
      Sangat Gampang
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
      dv1
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
      1
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
      1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
      dv2
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
      1
    </td>
    
    <td class="xl63">
      1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl67">
      (0,0)
    </td>
    
    <td class="xl67">
      (1,0)
    </td>
    
    <td class="xl67">
      (0,1)
    </td>
    
    <td class="xl67">
      (1,1)
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
    </td>
  </tr>
  
  <tr style="height: 45.0pt;">
    <td class="xl66" style="height: 45.0pt; width: 48pt;" width="64" height="60">
      Kepuasan
    </td>
    
    <td class="xl66" style="width: 48pt;" width="64">
      Sangat Tidak Puas
    </td>
    
    <td class="xl66" style="width: 48pt;" width="64">
      Tidak Puas
    </td>
    
    <td class="xl66" style="width: 48pt;" width="64">
      Puas
    </td>
    
    <td class="xl66" style="width: 48pt;" width="64">
      Sangat Puas
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
      dv1
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
      1
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
      1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
      dv2
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
    </td>
    
    <td class="xl63">
      1
    </td>
    
    <td class="xl63">
      1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl67">
      (0,0)
    </td>
    
    <td class="xl67">
      (1,0)
    </td>
    
    <td class="xl67">
      (0,1)
    </td>
    
    <td class="xl67">
      (1,1)
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  Tranformasi data diatas didapat dari pola <em><strong>Binary Table N bit</strong></em> seperti dibawah ini :
</p>

<table style="border-collapse: collapse; width: 603px; height: 405px;" border="0" width="256" cellspacing="0" cellpadding="0">
  <colgroup> <col style="width: 48pt;" width="64" /> <col style="width: 48pt;" span="3" width="64" /> </colgroup> <tr style="height: 15.0pt;">
    <td class="xl66" style="height: 15pt; width: 192pt; text-align: center;" colspan="4" width="256" height="20">
      Dummy Variable = n bit binary table
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td style="height: 15pt; text-align: center;" height="20">
      dvn = 2^n
    </td>
    
    <td class="xl65" style="text-align: center;">
      dv3
    </td>
    
    <td class="xl65" style="text-align: center;">
      dv2
    </td>
    
    <td class="xl65" style="text-align: center;">
      dv1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl65" style="text-align: center;">
    </td>
    
    <td class="xl65" style="text-align: center;">
    </td>
    
    <td class="xl65" style="text-align: center;">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl65" style="text-align: center;">
    </td>
    
    <td class="xl65" style="text-align: center;">
    </td>
    
    <td class="xl65" style="text-align: center;">
      1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl65" style="text-align: center;">
    </td>
    
    <td class="xl65" style="text-align: center;">
      1
    </td>
    
    <td class="xl65" style="text-align: center;">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl65" style="text-align: center;">
    </td>
    
    <td class="xl65" style="text-align: center;">
      1
    </td>
    
    <td class="xl65" style="text-align: center;">
      1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl65" style="text-align: center;">
      1
    </td>
    
    <td class="xl65" style="text-align: center;">
    </td>
    
    <td class="xl65" style="text-align: center;">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl65" style="text-align: center;">
      1
    </td>
    
    <td class="xl65" style="text-align: center;">
    </td>
    
    <td class="xl65" style="text-align: center;">
      1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl65" style="text-align: center;">
      1
    </td>
    
    <td class="xl65" style="text-align: center;">
      1
    </td>
    
    <td class="xl65" style="text-align: center;">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl65" style="text-align: center;">
      1
    </td>
    
    <td class="xl65" style="text-align: center;">
      1
    </td>
    
    <td class="xl65" style="text-align: center;">
      1
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  Contoh pada Attribut Kampus (ITB, ITS, UGM, UI), maka bila memilih :
</p>

<li style="text-align: justify;">
  ITB, nilainya adalah <span class="lang:default decode:true crayon-inline ">(dv1,dv2) = (0,0)</span>
</li>
<li style="text-align: justify;">
  ITS, nilainya adalah <span class="lang:default decode:true crayon-inline ">(1,0)</span>
</li>
<li style="text-align: justify;">
  UGM, nilainya adalah <span class="lang:default decode:true crayon-inline ">(0,1)</span>
</li>
<li style="text-align: justify;">
  UI, nilainya adalah <span class="lang:default decode:true crayon-inline ">(1,1)</span>
</li>
<li style="text-align: justify;">
  Begitu juga seterusnya dengan attribut yang lainnya.
</li>

Silahkan amati kembali Excel diatas pada tab **Raw Data**, pahami terlebih dahulu sebelum masuk ke step selanjutnya karena step selanjutnya akan berisi perhitungan &#8211; perhitungan matematis. Mudahkan ? Bila sudah dipahami mari kita lanjutkan.

Setelah data dibuat menjadi vector, maka selanjutnya menormalisasikan data tersebut dan membuat _**Aggregate Data**_ dari seluruh _attribute_. Mari kita lihat data kita yang sekarang, seperti yang ditunjukkan oleh tabel dibawah ini :

<table style="height: 322px;" width="607">
  <tr>
    <td style="text-align: center;" colspan="6" width="566">
      Data Setelah di vector kan
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      <strong>Nama</strong>
    </td>
    
    <td style="text-align: center;">
      <strong>IPK</strong>
    </td>
    
    <td style="text-align: center;">
      <strong>Semester</strong>
    </td>
    
    <td style="text-align: center;">
      <strong>Kampus</strong>
    </td>
    
    <td style="text-align: center;" width="100">
      <strong>Tingkat Kesulitan</strong>
    </td>
    
    <td style="text-align: center;">
      <strong>Kepuasan</strong>
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      A
    </td>
    
    <td style="text-align: center;">
      3.00
    </td>
    
    <td style="text-align: center;">
      7
    </td>
    
    <td style="text-align: center;">
      (1,0)
    </td>
    
    <td style="text-align: center;">
      (0,0)
    </td>
    
    <td style="text-align: center;">
      (0,1)
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      B
    </td>
    
    <td style="text-align: center;">
      3.50
    </td>
    
    <td style="text-align: center;">
      5
    </td>
    
    <td style="text-align: center;">
      (0,0)
    </td>
    
    <td style="text-align: center;">
      (1,0)
    </td>
    
    <td style="text-align: center;">
      (1,1)
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      C
    </td>
    
    <td style="text-align: center;">
      3.40
    </td>
    
    <td style="text-align: center;">
      3
    </td>
    
    <td style="text-align: center;">
      (0,1)
    </td>
    
    <td style="text-align: center;">
      (0,1)
    </td>
    
    <td style="text-align: center;">
      (0,1)
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      D
    </td>
    
    <td style="text-align: center;">
      3.80
    </td>
    
    <td style="text-align: center;">
      6
    </td>
    
    <td style="text-align: center;">
      (1,0)
    </td>
    
    <td style="text-align: center;">
      (0,1)
    </td>
    
    <td style="text-align: center;">
      (1,1)
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      E
    </td>
    
    <td style="text-align: center;">
      3.00
    </td>
    
    <td style="text-align: center;">
      7
    </td>
    
    <td style="text-align: center;">
      (1,1)
    </td>
    
    <td style="text-align: center;">
      (0,0)
    </td>
    
    <td style="text-align: center;">
      (1,0)
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      F
    </td>
    
    <td style="text-align: center;">
      3.40
    </td>
    
    <td style="text-align: center;">
      5
    </td>
    
    <td style="text-align: center;">
      (0,0)
    </td>
    
    <td style="text-align: center;">
      (1,0)
    </td>
    
    <td style="text-align: center;">
      (0,1)
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  Selanjutnya kita akan menghitung <em>Distance Matrix</em> pada setiap attribut data. Karena attribute (IPK dan Semester) adalah numerik, maka penulis akan menggunakan <strong>Manhattan Distance</strong>.<a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/Manhattan_distance.png"><img class="aligncenter size-full wp-image-350" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/Manhattan_distance.png" alt="" width="148" height="78" /></a>
</p>

<p style="text-align: justify;">
  Selanjutnya, kita hitung Manhattan Distance dari Attribut IPK.
</p>

<table width="694">
  <tr>
    <td colspan="2" width="181">
      Manhattan Distance
    </td>
    
    <td width="98">
      3
    </td>
    
    <td width="88">
      3,5
    </td>
    
    <td width="100">
      3,4
    </td>
    
    <td width="99">
      3,8
    </td>
    
    <td width="64">
      3
    </td>
    
    <td width="64">
      3,4
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td>
      <strong>IPK</strong>
    </td>
    
    <td>
      <strong>A</strong>
    </td>
    
    <td>
      <strong>B</strong>
    </td>
    
    <td>
      <strong>C</strong>
    </td>
    
    <td>
      <strong>D</strong>
    </td>
    
    <td>
      <strong>E</strong>
    </td>
    
    <td>
      <strong>F</strong>
    </td>
  </tr>
  
  <tr>
    <td>
      3
    </td>
    
    <td>
      <strong>A</strong>
    </td>
    
    <td>
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
      0,4
    </td>
    
    <td>
      0,8
    </td>
    
    <td>
    </td>
    
    <td>
      0,4
    </td>
  </tr>
  
  <tr>
    <td>
      3,5
    </td>
    
    <td>
      <strong>B</strong>
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
    </td>
    
    <td>
      0,1
    </td>
    
    <td>
      0,3
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
      0,1
    </td>
  </tr>
  
  <tr>
    <td>
      3,4
    </td>
    
    <td>
      <strong>C</strong>
    </td>
    
    <td>
      0,4
    </td>
    
    <td>
      0,1
    </td>
    
    <td>
    </td>
    
    <td>
      0,4
    </td>
    
    <td>
      0,4
    </td>
    
    <td>
    </td>
  </tr>
  
  <tr>
    <td>
      3,8
    </td>
    
    <td>
      <strong>D</strong>
    </td>
    
    <td>
      0,8
    </td>
    
    <td>
      0,3
    </td>
    
    <td>
      0,4
    </td>
    
    <td>
    </td>
    
    <td>
      0,8
    </td>
    
    <td>
      0,4
    </td>
  </tr>
  
  <tr>
    <td>
      3
    </td>
    
    <td>
      <strong>E</strong>
    </td>
    
    <td>
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
      0,4
    </td>
    
    <td>
      0,8
    </td>
    
    <td>
    </td>
    
    <td>
      0,4
    </td>
  </tr>
  
  <tr>
    <td>
      3,4
    </td>
    
    <td>
      <strong>F</strong>
    </td>
    
    <td>
      0,4
    </td>
    
    <td>
      0,1
    </td>
    
    <td>
    </td>
    
    <td>
      0,4
    </td>
    
    <td>
      0,4
    </td>
    
    <td>
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td>
      Max
    </td>
    
    <td>
      0,8
    </td>
    
    <td>
    </td>
    
    <td>
      Min
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  Darimana didapat angka-angka tersebut ? Dari kolom A ke bawah, didapat dari :
</p>

<li style="text-align: justify;">
  (A, A) = abs(3 &#8211; 3) = absolut(0) = 0
</li>
<li style="text-align: justify;">
  (A, B) = abs(3 &#8211; 3.5) = absolut(-0.5) = 0.5
</li>
<li style="text-align: justify;">
  (A, C) = abs(3 &#8211; 3.4) = 0.4
</li>
<li style="text-align: justify;">
  (A, D) = abs(3 &#8211; 3.8) = 0.8
</li>
<li style="text-align: justify;">
  (A, E) = abs(3 &#8211; 3) = 0
</li>
<li style="text-align: justify;">
  (A, F) = abs(3 &#8211; 3.4) = 0.4
</li>
<li style="text-align: justify;">
  Dan seterusnya sama halnya dengan attribut Semester.
</li>

Selanjutnya kita hitung Distance Matrix dari Attribute (Kampus, Tingkat Kesulitan, Kepuasan). Karena attribut tersebut berupa koordinat, maka penulis akan menerapkan _**Hamming Distance**_ pada ketiganya.

<table width="694">
  <tr>
    <td colspan="2" width="181">
      Hamming Distance
    </td>
    
    <td width="98">
      (1,0)
    </td>
    
    <td width="88">
      (0,0)
    </td>
    
    <td width="100">
      (0,1)
    </td>
    
    <td width="99">
      (1,0)
    </td>
    
    <td width="64">
      (1,1)
    </td>
    
    <td width="64">
      (0,0)
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td>
      <strong>Kampus</strong>
    </td>
    
    <td>
      <strong>A</strong>
    </td>
    
    <td>
      <strong>B</strong>
    </td>
    
    <td>
      <strong>C</strong>
    </td>
    
    <td>
      <strong>D</strong>
    </td>
    
    <td>
      <strong>E</strong>
    </td>
    
    <td>
      <strong>F</strong>
    </td>
  </tr>
  
  <tr>
    <td>
      (1,0)
    </td>
    
    <td>
      <strong>A</strong>
    </td>
    
    <td>
    </td>
    
    <td>
      1
    </td>
    
    <td>
      2
    </td>
    
    <td>
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
  </tr>
  
  <tr>
    <td>
      (0,0)
    </td>
    
    <td>
      <strong>B</strong>
    </td>
    
    <td>
      1
    </td>
    
    <td>
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      2
    </td>
    
    <td>
    </td>
  </tr>
  
  <tr>
    <td>
      (0,1)
    </td>
    
    <td>
      <strong>C</strong>
    </td>
    
    <td>
      2
    </td>
    
    <td>
      1
    </td>
    
    <td>
    </td>
    
    <td>
      2
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
  </tr>
  
  <tr>
    <td>
      (1,0)
    </td>
    
    <td>
      <strong>D</strong>
    </td>
    
    <td>
    </td>
    
    <td>
      1
    </td>
    
    <td>
      2
    </td>
    
    <td>
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
  </tr>
  
  <tr>
    <td>
      (1,1)
    </td>
    
    <td>
      <strong>E</strong>
    </td>
    
    <td>
      2
    </td>
    
    <td>
      2
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
    </td>
    
    <td>
      2
    </td>
  </tr>
  
  <tr>
    <td>
      (0,0)
    </td>
    
    <td>
      <strong>F</strong>
    </td>
    
    <td>
      1
    </td>
    
    <td>
    </td>
    
    <td>
      1
    </td>
    
    <td>
      1
    </td>
    
    <td>
      2
    </td>
    
    <td>
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td>
      Max
    </td>
    
    <td>
      2
    </td>
    
    <td>
    </td>
    
    <td>
      Min
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
    
    <td>
    </td>
  </tr>
</table>

Bagaimana formula dari Hamming Distance ? formulanya sebagai berikut :[<img class="aligncenter size-full wp-image-349" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/Hamming_distance.png" alt="" width="149" height="86" />](https://ekojunaidisalam.com/wp-content/uploads/2017/02/Hamming_distance.png)Setiap xor data yang bukan 0, atau setiap data <span class="lang:default decode:true crayon-inline ">x(i,j) ≠ x(j,k)</span>  maka jumlahkan nilainya. Contoh hasil dari attribut Kampus sebagai berikut :

<table style="border-collapse: collapse; width: 359px; height: 663px;" border="0" width="192" cellspacing="0" cellpadding="0">
  <colgroup> <col style="width: 48pt;" span="3" width="64" /> </colgroup> <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 30pt; width: 48pt; text-align: center;" rowspan="2" width="64" height="40">
      (A, A)
    </td>
    
    <td class="xl63" style="width: 48pt; text-align: center;" width="64">
      1
    </td>
    
    <td class="xl63" style="width: 48pt; text-align: center;" width="64">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15pt; text-align: center;" height="20">
      1
    </td>
    
    <td class="xl63" style="text-align: center;">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl63" style="text-align: center;" colspan="2">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 30pt; text-align: center;" rowspan="2" height="40">
      (A, B)
    </td>
    
    <td class="xl63" style="text-align: center;">
      1
    </td>
    
    <td class="xl63" style="text-align: center;">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15pt; text-align: center;" height="20">
    </td>
    
    <td class="xl63" style="text-align: center;">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl63" style="text-align: center;" colspan="2">
      1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 30pt; text-align: center;" rowspan="2" height="40">
      (A, C)
    </td>
    
    <td class="xl63" style="text-align: center;">
      1
    </td>
    
    <td class="xl63" style="text-align: center;">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15pt; text-align: center;" height="20">
    </td>
    
    <td class="xl63" style="text-align: center;">
      1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl63" style="text-align: center;" colspan="2">
      2
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 30pt; text-align: center;" rowspan="2" height="40">
      (A, D)
    </td>
    
    <td class="xl63" style="text-align: center;">
      1
    </td>
    
    <td class="xl63" style="text-align: center;">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15pt; text-align: center;" height="20">
      1
    </td>
    
    <td class="xl63" style="text-align: center;">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl63" style="text-align: center;" colspan="2">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 30pt; text-align: center;" rowspan="2" height="40">
      (A, E)
    </td>
    
    <td class="xl63" style="text-align: center;">
      1
    </td>
    
    <td class="xl63" style="text-align: center;">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15pt; text-align: center;" height="20">
      1
    </td>
    
    <td class="xl63" style="text-align: center;">
      1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl63" style="text-align: center;" colspan="2">
      1
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 30pt; text-align: center;" rowspan="2" height="40">
      (A, F)
    </td>
    
    <td class="xl63" style="text-align: center;">
      1
    </td>
    
    <td class="xl63" style="text-align: center;">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15pt; text-align: center;" height="20">
    </td>
    
    <td class="xl63" style="text-align: center;">
    </td>
  </tr>
  
  <tr style="height: 15.0pt;">
    <td class="xl63" style="height: 15.0pt;" height="20">
    </td>
    
    <td class="xl63" style="text-align: center;" colspan="2">
      1
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  Begitu juga untuk attribut Tingkat Kesulitan dan Kepuasan. Perhatikan kembali Excel diatas pada tab <strong>Vector</strong>. Silahkan scroll pada excel digeser ke kanan untuk melihat Normalisasi pada setiap attribut. Silahkan di pahami terlebih dahulu excel tersebut kemudian kita lanjut ke step berikutnya.
</p>

Setelah kita hitung Distance Matrix nya, kita buat normalisasi datanya, dengan formula sebagai berikut : [<img class="aligncenter size-full wp-image-352" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/norm.png" alt="" width="149" height="63" />](https://ekojunaidisalam.com/wp-content/uploads/2017/02/norm.png)

  * (A, A) = (0 &#8211; 0) / (0.8 &#8211; 0) = 0
  * (A, B) = (0.5 &#8211; 0) / (0.8 &#8211; 0) = 0.625
  * (A, C) = (0.4 &#8211; 0) / (0.8 &#8211; 0) = 0.5
  * (A, D) = (0.8 &#8211; 0) / (0.8 &#8211; 0) = 1
  * (A, E) = (0 &#8211; 0) / (0.8 &#8211; 0) = 0
  * (A, F) = (0.4 &#8211; 0) / (0.8 &#8211; 0) = 0.5
  * Dan seterusnya pada kolom dan attribut lainnya.

Sehingga hasilnya sebagai berikut untuk attribut IPK :

<table width="465">
  <tr>
    <td colspan="2" width="145">
      Normalize Distance
    </td>
    
    <td width="64">
    </td>
    
    <td width="64">
    </td>
    
    <td width="64">
    </td>
    
    <td width="64">
    </td>
    
    <td width="64">
    </td>
  </tr>
  
  <tr>
    <td>
      IPK
    </td>
    
    <td>
      A
    </td>
    
    <td>
      B
    </td>
    
    <td>
      C
    </td>
    
    <td>
      D
    </td>
    
    <td>
      E
    </td>
    
    <td>
      F
    </td>
  </tr>
  
  <tr>
    <td>
      A
    </td>
    
    <td>
    </td>
    
    <td>
      0,625
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
      1
    </td>
    
    <td>
    </td>
    
    <td>
      0,5
    </td>
  </tr>
  
  <tr>
    <td>
      B
    </td>
    
    <td>
      0,625
    </td>
    
    <td>
    </td>
    
    <td>
      0,125
    </td>
    
    <td>
      0,375
    </td>
    
    <td>
      0,625
    </td>
    
    <td>
      0,125
    </td>
  </tr>
  
  <tr>
    <td>
      C
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
      0,125
    </td>
    
    <td>
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
    </td>
  </tr>
  
  <tr>
    <td>
      D
    </td>
    
    <td>
      1
    </td>
    
    <td>
      0,375
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
    </td>
    
    <td>
      1
    </td>
    
    <td>
      0,5
    </td>
  </tr>
  
  <tr>
    <td>
      E
    </td>
    
    <td>
    </td>
    
    <td>
      0,625
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
      1
    </td>
    
    <td>
    </td>
    
    <td>
      0,5
    </td>
  </tr>
  
  <tr>
    <td>
      F
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
      0,125
    </td>
    
    <td>
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
    </td>
  </tr>
</table>

Nilai Aggregate didapat dari jumlah seluruh data yang telah dinormalisasi. Contoh : (A, A) = IPK(A, A) + Semester(A, A) + Kampus(A, A) + Tingkat Kesulitan(A, A) + Kepuasan(A,A)

Sehingga didapat Aggregate data sebagai berikut :

<table width="694">
  <tr>
    <td colspan="2" width="181">
      Aggregation
    </td>
    
    <td width="98">
    </td>
    
    <td width="88">
    </td>
    
    <td width="100">
    </td>
    
    <td width="99">
    </td>
    
    <td width="64">
    </td>
    
    <td width="64">
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td>
      Sum
    </td>
    
    <td>
      A
    </td>
    
    <td>
      B
    </td>
    
    <td>
      C
    </td>
    
    <td>
      D
    </td>
    
    <td>
      E
    </td>
    
    <td>
      F
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td>
      A
    </td>
    
    <td>
    </td>
    
    <td>
      2,625
    </td>
    
    <td>
      4
    </td>
    
    <td>
      1,75
    </td>
    
    <td>
      1
    </td>
    
    <td>
      2,5
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td>
      B
    </td>
    
    <td>
      2,625
    </td>
    
    <td>
    </td>
    
    <td>
      2,625
    </td>
    
    <td>
      2,625
    </td>
    
    <td>
      3,625
    </td>
    
    <td>
      0,125
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td>
      C
    </td>
    
    <td>
      4
    </td>
    
    <td>
      2,625
    </td>
    
    <td>
    </td>
    
    <td>
      3,25
    </td>
    
    <td>
      3
    </td>
    
    <td>
      2,5
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td>
      D
    </td>
    
    <td>
      1,75
    </td>
    
    <td>
      2,625
    </td>
    
    <td>
      3,25
    </td>
    
    <td>
    </td>
    
    <td>
      2,75
    </td>
    
    <td>
      2,75
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td>
      E
    </td>
    
    <td>
      1
    </td>
    
    <td>
      3,625
    </td>
    
    <td>
      3
    </td>
    
    <td>
      2,75
    </td>
    
    <td>
    </td>
    
    <td>
      3,5
    </td>
  </tr>
  
  <tr>
    <td>
    </td>
    
    <td>
      F
    </td>
    
    <td>
      2,5
    </td>
    
    <td>
      0,125
    </td>
    
    <td>
      2,5
    </td>
    
    <td>
      2,75
    </td>
    
    <td>
      3,5
    </td>
    
    <td>
    </td>
  </tr>
</table>

Hasil rata &#8211; rata data Aggregate :

<table width="619">
  <tr>
    <td width="106">
      Average Distance
    </td>
    
    <td width="98">
      A
    </td>
    
    <td width="88">
      B
    </td>
    
    <td width="100">
      C
    </td>
    
    <td width="99">
      D
    </td>
    
    <td width="64">
      E
    </td>
    
    <td width="64">
      F
    </td>
  </tr>
  
  <tr>
    <td>
      A
    </td>
    
    <td>
    </td>
    
    <td>
      0,525
    </td>
    
    <td>
      0,8
    </td>
    
    <td>
      0,35
    </td>
    
    <td>
      0,2
    </td>
    
    <td>
      0,5
    </td>
  </tr>
  
  <tr>
    <td>
      B
    </td>
    
    <td>
      0,525
    </td>
    
    <td>
    </td>
    
    <td>
      0,525
    </td>
    
    <td>
      0,525
    </td>
    
    <td>
      0,725
    </td>
    
    <td>
      0,025
    </td>
  </tr>
  
  <tr>
    <td>
      C
    </td>
    
    <td>
      0,8
    </td>
    
    <td>
      0,525
    </td>
    
    <td>
    </td>
    
    <td>
      0,65
    </td>
    
    <td>
      0,6
    </td>
    
    <td>
      0,5
    </td>
  </tr>
  
  <tr>
    <td>
      D
    </td>
    
    <td>
      0,35
    </td>
    
    <td>
      0,525
    </td>
    
    <td>
      0,65
    </td>
    
    <td>
    </td>
    
    <td>
      0,55
    </td>
    
    <td>
      0,55
    </td>
  </tr>
  
  <tr>
    <td>
      E
    </td>
    
    <td>
      0,2
    </td>
    
    <td>
      0,725
    </td>
    
    <td>
      0,6
    </td>
    
    <td>
      0,55
    </td>
    
    <td>
    </td>
    
    <td>
      0,7
    </td>
  </tr>
  
  <tr>
    <td>
      F
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
      0,025
    </td>
    
    <td>
      0,5
    </td>
    
    <td>
      0,55
    </td>
    
    <td>
      0,7
    </td>
    
    <td>
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  Setelah data diubah menjadi vector selanjutnya data dapat diolah untuk di cluster menggunakan K-Means Clusterig. Silahkan gunakan aplikasi pada <a href="https://ekojs.github.io/ejs_k-means/" target="_blank">link berikut</a> dengan data <span class="lang:default decode:true crayon-inline ">nxm dimension = 6,2</span>  dan <span class="lang:default decode:true crayon-inline">samples = 0,0.525,0.8,0.35,0.2,0.5,0.525,0,0.525,0.525,0.725,0.025,0.8,0.525,0,0.65,0.6,0.5,0.35,0.525,0.65,0,0.55,0.55,0.2,0.725,0.6,0.55,0,0.7,0.5,0.025,0.5,0.55,0.7,0</span>  sedangkan centroids dikosongkan saja. Silahkan dicoba bila dicluster sebanyak 3 atau 4, dsb. Untuk excel embedded silahkan di full view dengan klik ikon pojok kanan bawah excel tersebut.
</p>

Bila ada pertanyaan atau diskusi seputar K-Means Clustering pada Multivariate Data berikut, silahkan komentar. Terima kasih. 😀
