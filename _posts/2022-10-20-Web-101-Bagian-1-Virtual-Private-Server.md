---
title: Web 101 Bagian 1 -Virtual Private Server
date: 2022-10-20 13:07:00 +0700
categories: [Blogging, Tutorial]
tags: [vps, virtual private server, digital ocean, debian, hosting, web]
---

## Apa Itu Virtual Private Server

Server secara sederhana adalah sebuah komputer yang secara konstan selalu terhubung ke internet dan menyediakan beberapa layanan internet salah satunya adalah http. Agar situs web kamu bisa diakses melalui jaringan internet maka diperlukannya sebuah server yang nantinya akan di pasang web server.

Memiliki server yang terkoneksi dengan internet sangat-sangat berguna walaupun nanti di server tersebut kamu tidak menghost website kamu. Dengan server yang terkoneksi di internet kamu bisa membuat situs web, email, layanan berbagi file, dns dan banyak hal lainnya.

Virtual Private Server atau disingkat VPS adalah salah satu cara untuk mendapatkan server web yang murah dan cepat, dibanding dengan membangun server sendiri di rumah, kamu tidak perlu repot membeli peralatan pc server yang mahal, memikirkan listrik bulanan untuk server kamu, dan biaya internetnya.

Ada beberapa perusahaan yang mempunyai bisnis online di mana mereka mempunyai komputer server yang banyak dengan spesifikasi yang bagus, internet kencang dan daya listrik yang besar. Kemudian perusahaan tersebut menyewakan server mereka ke kamu dengan harga yang cukup terjangkau.

Biasanya harga VPS yang mereka tawarkan paling murah berkisar antara 50 ribu hingga 100 ribu perbulan, dipandang dari uang saku harga itu sudah cukup terjangkau. Dengan harga segitu kamu bisa menghost banyak website dan beberapa layanan dalam satu VPS. Sebagai contoh bisa saja dalam satu VPS itu kamu menginstall selusin situs web, server email, dan file sharing.

Penyedia VPS yang akan aku gunakan dalam panduan ini adalah DigitalOcean.

## Membeli VPS

Pertama [buat akun DigitalOcean di sini](https://m.do.co/c/e1d9555fa230) dan mari kita mulai.

Kebanyakan penyedia layanan VPS akan memberikan pilihan di mana letak secara geografis dari server tersebut yang ingin kamu sewa.

**Lokasi Server**

Untuk memilih lokasi server pastikan lokasi yang kamu pilih itu dekat dengan lokasi kamu berada saat ini, misalnya aku berada di Riau yang dekat dengan Singapura maka aku akan memilih lokasi server yang berada di Singapura. Tapi jika kamu ingin membuat website di mana kamu menargetkan web tersebut diakses oleh orang India ada baiknya jika lokasi server yang kamu pilih di Bangalore.

![Lokasi Server](/posts/20221020/01-lokasi-server.png)

**Sistem Operasi**

![Sistem Operasi Yang Di Pilih](/posts/20221020/02-sistem-operasi.png)

Untuk sistem operasi server aku merekomendasikan kamu untuk menggunakan **Debian 11**. Debian adalah salah satu sistem operasi untuk server yang cukup tua dan stabil, lagipula panduan ini juga akan menggunakan **Debian 11**. Jika kamu menggunakan sistem operasi lain, mungkin terdapat beberapa perbedaan instruksi nantinya di terminal.

**Ukuran Server**

![Ukuran daripada server](/posts/20221020/03-ukuran-server.png)

Pada bagian ini kamu dapat menyesuaikan spesifikasi dari server kamu, pada panduan ini aku memilih spesifikasi 1GB/1CPU/25GB dengan tipe droplet _Basic_

Untuk menghosting sebuah web atau bahkan situs yang cukup rumit tidaklah terlalu menggunakan sumber daya RAM atau CPU yang sangat besar. Tapi jika nantinya kamu mau melakukan hal-hal yang lebih berat daripada menghosting beberapa halaman web dan semacamnya, kamu bisa mengupgrade spesifikasi server kamu nanti di DigitalOcean.

**Kata Sandi**

![Membuat kata sandi](/posts/20221020/04-kata-sandi.png)

Setelah itu silahkan kamu membuat kata sandi untuk VPS kamu agar nanti kamu bisa masuk ke server kamu menggunakan _SSH_. Walaupun sebenarnya kamu bisa menggunakan metode autentikasi lain seperti menggunakan SSH Key. Tapi pada panduan ini mari menggunakan kata sandi saja terlebih dahulu.

**Hostname dan Selesai**

![Hostname dan create droplets](/posts/20221020/05-hostname-done.png)

Setelah itu silahkan mengganti `hostname menjadi debian11` dan klik `Create Droplet`, maka setelah itu silahkan tunggu, server kamu akan segera otomatis di deploy oleh DigitalOcean. Dan setelah selesai nanti kamu akan segera bisa melihat alamat IP dari server kamu.
