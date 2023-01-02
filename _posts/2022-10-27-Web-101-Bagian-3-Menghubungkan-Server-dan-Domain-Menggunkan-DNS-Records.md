---
title: Web 101 Bagian 3 - Menghubungkan Server dan Domain Menggunkan DNS Records
date: 2022-10-27 13:17:00 +0700
categories: [Blogging, Tutorial]
tags: [dns record, domainesia, vps, AAA]
---

## Rangkuman
Sekarang kita sudah memiliki [nama domain](https://anggra.id/posts/Web-101-Bagian-2-Domain-Name/) dan
[server](https://anggra.id/posts/Web-101-Bagian-1-Virtual-Private-Server/), cara terbaik untuk menghubungkan keduanya
adalah dengan menggunakan rekaman DNS atau *DNS records*. Rekaman DNS (*domain name system*) biasanya ditambahkan di
registar agar  orang yang mencari situs webmu melalui domain dapat terhubung ke server tempat situs webmu berada.
Sehingga orang dapat menemukan webmu dengan mudah tanpa perlu mengingat alamat ip servermu.

Untuk menghubungkan nama domain dan server, ambil alamat IPv4/IPv6 kamu dari DigitalOcean dan masukkan ke dalam rekaman
A/AAAA di Domainesia. Proses ini mudah dilakukan dan hanya membutuhkan waktu kurang lebih satu menit. Berikut
langkah-langkahnya disertai gambar.

## Buka Registrar
Seperti postingan sebelumnya, kita akan menggunakan Domainesia sebagai registrar dan DigitalOcean sebagai penyedia vps.
Masuk ke akunmu di kedua layanan tersebut. Kemudian buka Domainesia atau registar yang kamu pakai, kemudian klik pada
nama domainmu dan pilih "DNS Management". Berikut tampilan DNS Management tersebut

![tampilan dns managemnt](/posts/20221027/01-buka.png)

Secara default beginilah tampilan dari DNS Management. Yang harus kita lakukan sekarang adalah mengcopy alamat IP server
kita dari DigitalOcean dan menambahkan rekaman DNS baru yang akan menghubungkan koneksi ke server kita.

## Copy IP Address Server
Untuk mendapatkan alamat IP dari DigitalOcean, klik pada droplet yang telah kamu buat. Kemudian, perhatikan di sisi kiri menu,
kamu akan melihat sebuah angka seperti contohnya 104.248.159.148. Itulah alamat IPv4 dari servermu.

![alamat ipv4](/posts/20221027/02-cari-ip.png)

Copy alamat IPv4mu dan di Domainesia, tambahkan dua entri A dengan contoh seperti berikut, untuk memasukkan
datanya harus perbaris satu-satu tekan save changes.

![done ipv4](/posts/20221027/03-ipv4-done.png)

aku menambahkan dua entri. Satu diantaranya memiliki tanda @ di bagian "Host Name". Record ini akan mengarahkan
koneksi ang.my.id melalui IPv4 ke alamat IP server kita. Entri yang lain memiliki tanda * di bagian "Host Name".
Record ini akan mengarahkan semua koneksi yang datang ke subdomain akan diarahkan ke tempat alamat ip yang sama yaitu
104.248.159.148, misalnya www.ang.my.id, mail.ang.my.id, dll akan ke mengarah ke situ.

Kemudian mari kita menambahkan alamat IPv6 kita, untuk mendapatkannya agak sedikit membutuhkan kerja keras, karena secara
default alamatnya di nonaktifkan. IPv6 sangat penting karena kita sedang kehabisan IPv4, jadi sangat penting untuk memungkinkan
koneksi melalui IPv6 karena akan menjadi standar di masa depan.

Pada droplet, klik bagian "networking" kemudian akan muncul tulisan untuk mengaktifkan IPv6 droplet perlu dimatikan terlebih dahulu,
silahkan klik "Turn off".

![matikan droplet](/posts/20221027/04-turn-on-ipv6.png)

Kemudian setelah droplet mati, tampilan akan berubah dan kita sekarang bisa menyalakan alamat IPv6

![hidupkan ipv6](/posts/20221027/05-enable-ipv6.png)

Setelah dinyalakan maka akan muncul sekumpulan angka dan huruf yang jelek dengan tanda titik dua di antaranya
(2400:6180:0:d0::137c:7001) dan ini adalah alamat IPv6 saya. Alamat IPv6 kamu akan terlihat seperti itu.

![alamat ipv6](/posts/20221027/07-tampilan-ipv6.png)

Sekarang masuk ke Domainesia. Kali ini, pastikan untuk memilih menambahkan rekaman AAAA seperti yang ditunjukkan dibawah
ini:

![record AAAA](/posts/20221027/06-ipv6-done.png)

Setelah kamu simpan, maka proses menambahkan record dns sudah selesai.

## Mari Kita Tes!!
Sekarang kita seharusnya memiliki nama domain yang mengarah ke ip server kita. Kita dapat memeriksanya dengan cara
melakukan ping nama domain kita, seperti gambar di bawah

![ping](/posts/20221027/08-ping.png)

Seperti yang kamu lihat, ping ke ang.my.id sekarang diarahkan ke 104.248.159.148. Ini berarti kita berhasil mengatur
record DNS kita! Kamu juga bisa menjalankan perintah `host ang.my.id`, yang akan menampilkan alamat IPv4 dan IPv6
dari nama domain ang.my.id

