---
title: Mengganti Layout IME Jepang Menjadi DVORAK
date: 2024-07-24 12:25:00 +0700
categories: [Panduan]
tags: [windows, jepang]
---

Beberapa minggu yang lalu aku mencoba untuk belajar Bahasa Jepang, dari saran yang kutemukan kebanyakan menekankan harus
mempelajari sistem penulisan dasar yaitu Katakana dan Hiragana terlebih dahulu. Sehingga mulailah aku mencari referensi
yang bagus untuk belajar cara membaca dua sistem penulisan ini.

Akhirnya aku menemukan website yang cocok yaitu Tofugu.com. Di sini mempelajari setiap karakternya menggunakan sistem
mnemonic disertai ilustrasi gambar. Jujur aku suka dengan website ini dan aku sangat merekomendasikannya kalau kamu
ingin belajar Katakana atau Hiragana.

![](/posts/20240724/belajar-hiragana-tofugu.png)

Untuk belajar Hiragana kamu dapat mengunjungi link berikut Learn Hiragana: Tofugu's Ultimate Guide sedangkan Katakana di
[Hiragana](https://www.tofugu.com/japanese/learn-hiragana/) dan [Katakana](https://www.tofugu.com/japanese/learn-katakana/).

![](/posts/20240724/belajar-katakana-tofugu.png)

Setelah lancar dan dikatakan cukup mahir membaca sistem tulisan itu, aku hendak menambahkan layout keyboard tersebut ke
komputerku. Karena aku cukup sering mengubah layout di komputer ini jadi aku tinggal menambahkan Bahasa Jepang saja di
pengaturan, secara otomatis seharusnya akan muncul layout keyboard tsb.

![](/posts/20240724/menambahkan-bahasa-jepang.png)

Namun masalah baru muncul, secara bawaan IME input Bahasa Jepang ini menggunakan layout QWERTY sedangkan aku mahir di
DVORAK, ini sangat menyulitakan terlebih aku mengetik QWERTY cukup lambat dibanding DVORAK yang bisa diatas 100+wpm.

Setelah merenung beberapa lama, aku terpikir mengapa tidak mengubah di bagian registry saja. Pertama aku searching dan
menemukan untuk menemukan registry keyboard Jepang aku dapat menemukannnya di
`Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters`{: .filepath }

![](/posts/20240724/before-keyboard-ime-change-to-dvorak-1.png)

Akhirnya ketemu, pada bagian LayerDriver JPN ini kuubah isi datanya dengan cara klik dua kali.

![](/posts/20240724/change-to-dvorak.png)

Kemudian mengganti isinya  dengan layout dvorak, karena aku sering aku sudah cukup hafal dengan kode layout ini yaitu
kbddvp.dll setelah itu aku klik OK dan merestart komputer. Setelah itu langsung ku tes dan hasilnya berhasil! Kini
layout IME Jepang ini menjadi layout DVORAK.

Demikian pengalaman singkat ini yang sengaja kutulis dengan maksud agar jika suatu saat aku hendak mengkonfigurasi
komputer lain, aku tidak lupa jadi tinggal baca disini saja. Satu lagi untuk mengubah dari latin ke hiragna dapat
menekan tombol alt + ~.

ありがとうございます

