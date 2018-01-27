---
id: 323
title: K-Means Clustering Algorithm
date: 2017-02-09T21:26:56+00:00
author: Eko Junaidi Salam
layout: post
guid: http://ekojunaidisalam.com/?p=323
permalink: /2017/02/09/k-means-clustering-algorithm/
dsq_thread_id:
  - "5536434383"
dsq_needs_sync:
  - "1"
categories:
  - Algorithm
  - Artikel
  - Data Science
  - Programming
  - Teknologi
tags:
  - Data Mining
  - Data Science
  - Euclidean Distance
  - K-Means Algorithm
  - K-Means Clustering
---
<h2 style="text-align: center;">
  <a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/ejs_k_means.png"><img class="aligncenter wp-image-325 size-large" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/ejs_k_means-1024x524.png" alt="K-Means Clustering" width="584" height="299" srcset="https://ekojunaidisalam.com/wp-content/uploads/2017/02/ejs_k_means-1024x524.png 1024w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/ejs_k_means-300x153.png 300w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/ejs_k_means-768x393.png 768w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/ejs_k_means-500x256.png 500w" sizes="(max-width: 584px) 100vw, 584px" /></a>K-Means Clustering
</h2>

<p style="text-align: justify;">
  K-Means Clustering adalah salah satu algoritma dalam menentukan klasifikasi terhadap objek berdasarkan attribut / fitur dari objek tersebut kedalam <strong>K</strong> kluster/partisi. K adalah angka positif yang menyatakan jumlah grup/kluster/partisi terhadap objek. Pemartisian data dilakukan dengan mencari nilai jarak minimum antara data dan nilai <em><strong>centroid</strong> </em>yang telah di set baik secara random atau pun dengan<em><strong> Initial Set of Centroids, </strong></em>kita juga dapat menentukan nilai centroid berdasarkan <strong>K object</strong> yang berurutan.
</p>

<p style="text-align: justify;">
  <a href="https://en.wikipedia.org/wiki/Centroid" target="_blank" rel="noopener noreferrer"><em><strong>Centroid</strong> </em></a>adalah nilai rata-rata aritmetik dari sebuah bentuk objek dari seluruh titik dalam objek tersebut. Penerapan K-Means Clustering ini dapat dilakukan dengan prosedur <em>step by step</em> berikut :
</p>

<li style="text-align: justify;">
  Siapkan data training berbentuk vector.
</li>
<li style="text-align: justify;">
  Set nilai K cluster.
</li>
<li style="text-align: justify;">
  Set nilai awal centroids.
</li>
<li style="text-align: justify;">
  Hitung jarak antara data dan centroid menggunakan rumus <a href="https://en.wikipedia.org/wiki/Euclidean_distance" target="_blank" rel="noopener noreferrer"><em><strong>Euclidean Distance</strong></em></a>.
</li>
<li style="text-align: justify;">
  Partisi data berdasarkan nilai minimum.
</li>
<li style="text-align: justify;">
  Kemudian lakukan iterasi selama partisi data masih bergerak (tidak ada lagi objek yang bergerak ke partisi lain), bila masih maka ke poin 3.
</li>
<li style="text-align: justify;">
  Bila grup data sekarang sama dengan grup data sebelumnya, maka hentikan iterasi.
</li>
<li style="text-align: justify;">
  Data telah dipartisi sesuai nilai centroid akhir.
</li>

<a name='more'></a>

<p style="text-align: center;">
  <a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/K-Means-Flow.png"><img class="size-medium wp-image-328 aligncenter" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/K-Means-Flow-300x297.png" alt="K-Means Clustering" width="300" height="297" srcset="https://ekojunaidisalam.com/wp-content/uploads/2017/02/K-Means-Flow-300x297.png 300w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/K-Means-Flow-150x150.png 150w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/K-Means-Flow-303x300.png 303w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/K-Means-Flow.png 343w" sizes="(max-width: 300px) 100vw, 300px" /></a>Contoh penerapan K-Means Cluster
</p>

<table width="242">
  <tr>
    <td style="text-align: center;" rowspan="2" width="114">
      <strong>Data</strong>
    </td>
    
    <td style="text-align: center;" colspan="2" width="128">
      <strong>Attribut / fitur</strong>
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      <strong>X</strong>
    </td>
    
    <td style="text-align: center;">
      <strong>Y</strong>
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      A
    </td>
    
    <td style="text-align: center;">
      5,09
    </td>
    
    <td style="text-align: center;">
      5,80
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      B
    </td>
    
    <td style="text-align: center;">
      3,24
    </td>
    
    <td style="text-align: center;">
      5,90
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      C
    </td>
    
    <td style="text-align: center;">
      1,68
    </td>
    
    <td style="text-align: center;">
      4,90
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      D
    </td>
    
    <td style="text-align: center;">
      1,00
    </td>
    
    <td style="text-align: center;">
      3,17
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      E
    </td>
    
    <td style="text-align: center;">
      1,48
    </td>
    
    <td style="text-align: center;">
      1,38
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      F
    </td>
    
    <td style="text-align: center;">
      2,91
    </td>
    
    <td style="text-align: center;">
      0,20
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      G
    </td>
    
    <td style="text-align: center;">
      4,76
    </td>
    
    <td style="text-align: center;">
      0,10
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      H
    </td>
    
    <td style="text-align: center;">
      6,32
    </td>
    
    <td style="text-align: center;">
      1,10
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      I
    </td>
    
    <td style="text-align: center;">
      7,00
    </td>
    
    <td style="text-align: center;">
      2,83
    </td>
  </tr>
  
  <tr>
    <td style="text-align: center;">
      J
    </td>
    
    <td style="text-align: center;">
      6,52
    </td>
    
    <td style="text-align: center;">
      4,62
    </td>
  </tr>
</table>

<p style="text-align: justify;">
  Akan dilakukan pemartisian data terhadap data diatas sebanyak 2 partisi, maka tahapannya dalah sebagai berikut :
</p>

<li style="text-align: justify;">
  K = 2, (K = Jumlah Cluster)
</li>
<li style="text-align: justify;">
  Nilai awal centroid (1.48,1.38) untuk partisi 0, dan centroid (4.76,0.10) untuk partisi 1
</li>
<li style="text-align: justify;">
  Maka perhitungan Euclidean Distance adalah <a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/Euclidean-Distance-1.png"><img class="aligncenter wp-image-331 size-full" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/Euclidean-Distance-1.png" width="187" height="89" /></a>dimana <em><strong>p</strong></em> adalah data, <em><strong>c</strong></em> adalah centroid, n adalah jumlah data, i adalah iterasi.
</li>
<li style="text-align: justify;">
  Hasil perhitungan jarak minimum A adalah <a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/a.png"><img class="aligncenter wp-image-332 size-full" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/a.png" width="351" height="68" srcset="https://ekojunaidisalam.com/wp-content/uploads/2017/02/a.png 351w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/a-300x58.png 300w" sizes="(max-width: 351px) 100vw, 351px" /></a>
</li>
<li style="text-align: justify;">
  Hasil perhitungan jarak minimum B adalah<a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/b.png"><img class="aligncenter wp-image-333 size-full" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/b.png" width="352" height="67" srcset="https://ekojunaidisalam.com/wp-content/uploads/2017/02/b.png 352w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/b-300x57.png 300w" sizes="(max-width: 352px) 100vw, 352px" /></a>
</li>
<li style="text-align: justify;">
  Hasil perhitungan jarak keseluruhan<a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/Min-Distance-0.png"><img class="aligncenter size-full wp-image-334" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/Min-Distance-0.png" alt="" width="193" height="225" /></a>
</li>
<li style="text-align: justify;">
  Hasil perhitungan partisi diambil dari jarak minimum, sehingga didapat sebagai berikut : <a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/Object-Clustering-0.png"><img class="aligncenter size-full wp-image-335" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/Object-Clustering-0.png" alt="" width="194" height="228" /></a>Contoh pada A, X = 5.707 lebih kecil dari Y = 5.710, maka A termasuk ke dalam Cluster 0. Begitu juga dengan F, X = 1.854 lebih besar dari Y = 1.853, maka B masuk ke dalam Cluster 1.
</li>
<li style="text-align: justify;">
  Setelah data di partisi, maka selanjutnya nilai centroid harus dihitung ulang untuk menentukan jarak minimum yang baru, berikut perhitungan centroid baru :<a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/new-centroid.png"><img class="aligncenter wp-image-336 size-full" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/new-centroid.png" width="613" height="181" srcset="https://ekojunaidisalam.com/wp-content/uploads/2017/02/new-centroid.png 613w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/new-centroid-300x89.png 300w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/new-centroid-500x148.png 500w" sizes="(max-width: 613px) 100vw, 613px" /></a>
</li>
<li style="text-align: justify;">
  Hitung jarak minimumnya kembali dengan menggunakan centroid yang baru, sehingga di dapat hasilnya sebagai berikut.<a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/Min-Distance-1.png"><img class="aligncenter size-full wp-image-337" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/Min-Distance-1.png" alt="" width="192" height="234" /></a>
</li>
<li style="text-align: justify;">
  Klasifikasikan kembali data berdasar jarak minimum diatas.<a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/Object-Clustering-0.png"><img class="aligncenter size-full wp-image-335" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/Object-Clustering-0.png" alt="" width="194" height="228" /></a>
</li>
<li style="text-align: justify;">
  Karena tidak ada data yang berpindah ke cluster yang berbeda, sehingga iterasi kita cukupkan sampai dengan nilai centroid akhir : <strong>(2.50,4.23), (5.50,1.77)</strong>
</li>

Berikut adalah tampilan kordinat cartesius dari sample data diatas :

<p style="text-align: center;">
  <a href="https://ekojunaidisalam.com/wp-content/uploads/2017/02/sample_data.png"><img class="aligncenter wp-image-339 size-full" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/sample_data.png" width="1008" height="728" srcset="https://ekojunaidisalam.com/wp-content/uploads/2017/02/sample_data.png 1008w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/sample_data-300x217.png 300w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/sample_data-768x555.png 768w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/sample_data-415x300.png 415w" sizes="(max-width: 1008px) 100vw, 1008px" /></a>
</p>

Berikut adalah tampilan setelah penerapan K-Means Clustering dengan centroid akhir:

[<img class="aligncenter wp-image-340 size-full" src="https://ekojunaidisalam.com/wp-content/uploads/2017/02/k-means_result.png" width="961" height="988" srcset="https://ekojunaidisalam.com/wp-content/uploads/2017/02/k-means_result.png 961w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/k-means_result-292x300.png 292w, https://ekojunaidisalam.com/wp-content/uploads/2017/02/k-means_result-768x790.png 768w" sizes="(max-width: 961px) 100vw, 961px" />](https://ekojunaidisalam.com/wp-content/uploads/2017/02/k-means_result.png)

Aplikasi K-Means Clustering sangat sering digunakan, mulai dari _unsupervised learning of neural network_, _Pattern Recognitions_, _Classifications Analysis_, _Artificial Intelligence_, _Image Processing_, _Computer Vision_ dan banyak lainnya.

Berikut adalah penerapan K-Means Clustering pada Bahasa Pemrograman JavaScript (spidermonkey). <a href="https://ekojs.github.io/2017/03/17/kmeans-clustering-algorithm.html" target="_blank" rel="noopener noreferrer">Sample Test Program !!!</a>

Apabila ada yang ingin didiskusikan, silahkan isi komentar yak. Sampai jumpa di artikel selanjutnya.

Source Code : <a href="https://github.com/ekojs/machine_learning/blob/master/unsupervised/ejs_kmeans.js" target="_blank" rel="noopener noreferrer">https://github.com/ekojs/machine_learning/blob/master/unsupervised/ejs_kmeans.js</a>

Sumber :

  * https://en.wikipedia.org/wiki/K-means_clustering
  * http://people.revoledu.com/kardi/tutorial/kMean/NumericalExample.htm
  * http://mnemstudio.org/clustering-k-means-introduction.htm
