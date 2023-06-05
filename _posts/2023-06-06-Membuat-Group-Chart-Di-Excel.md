---
title: Membuat Group Chart di Excel
date: 2023-06-06 03:01:00 +0700
categories: [Panduan]
tags: [Excel, chart, grouping]
---

Jadi beberapa minggu terakhir aku bingung bagaimana membuat chart
diagram batang di excel. Aku sudah search tapi tidak menemukan caranya,
hasilnya kebanyakan tidak sesuai dengan yang aku ingin. Aku sudah otak
atik hasilnya juga tidak sesuai harapan.

Mulai dari seperti ini.

![](/posts/20230606/image1.png)

Seperti ini.

![](/posts/20230606/image2.png)

Hingga seperti ini.

![](/posts/20230606/image3.png)

Jadi aku bertanya di komunitas excel di reddit, hasilnya aku menemukan
jawabannya. Di jawab oleh [Starwax (u/Starwax) -
Reddit](https://www.reddit.com/user/Starwax/) pada thread [Combine
multiple chart to one chart : excel
(reddit.com)](https://www.reddit.com/r/excel/comments/1418yfr/combine_multiple_chart_to_one_chart/)
hasilnya memuaskan. Aku sudah coba hasilnya seperti berikut.

![](/posts/20230606/image4.png)

Berhasil !!

Jadi ternyata Excel khususnya untuk chart membaca data dari kiri ke
kanan, semakin ke kiri maka yang kiri tersebut akan menjadi grup
kategori untuk data yang di bagian kanan. Sebagai contoh jika aku ingin
melakukan group untuk web dinamis dan statis maka aku bisa mengarrange
tabel tersebut seperti ini.

![](/posts/20230606/image5.png)

Terlihat akhirnya Excel membagi dua data tersebut ke dalam kategori yang
berbeda di chart tersebut. Untuk kolom Nginx dan Lighttpd harus
dibiarkan seperti itu agar batang-batang yang ada di chart melakukan
perbandingan. Tidak seperti video yang kutonton sebelumnya, yaitu ini,
yang datanya malah tidak melakukan perbandingan secara side to side di
setiap grouping.

[How to Create Multi-Category Column/Bar Chart in Excel -
YouTube](https://www.youtube.com/watch?v=zJynocLdpe8)
