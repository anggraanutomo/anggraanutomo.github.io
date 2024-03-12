---
title: Menghapus Permanen Dualboot Di Komputer
date: 2024-03-12 12:25:00 +0700
categories: [Panduan]
tags: [linux, efi, cmd, dualboot]
---

Pada tulisan ini aku akan membahas bagaimana cara menghapus permanent dualboot yang masih ada di menu boot.
Berawal dari sebelumnya di tahun 2019 aku pernah mencoba melakukan dualboot untuk Ubuntu dan Windows 10, tapi sayangnya
optimasinya kurang bagus. Baterai laptop ini semenjak dipakai menggunakan Ubuntu cepat sekali terkuras, dan masih
banyak yang harus diperbaiki secara manual seperti brightness yang harus di lakukan tweak agar muncul pengaturan
geser-geser brightnessnya dari gelap ke terang. Karena beberapa masalah itu aku memutuskan untuk menghapus partisinya
si Ubuntu tadi, nah setelah berhasil dihapus dan grub loadernya sudah tidak muncul saat laptop dinyalakan, pada hari ini
aku baru sadar bahwa Ubuntu ini belum benar-benar terhapus. Saat aku mengecek bios ternyata boot masih ada tertulis Ubuntu
disana.

Jika kamu mengalami masalah yang serupa silahkan ikuti proses-proses ini:

Pertama kamu harus melihat pada bagian disk management (cara masuk ke disk management ketik di search windows disk management)
, cari disitu label partisi efi dan ingat berapa ukurannya, seharusnya ukurannya tidak lebih dari 1 GB, pada kasusku
ukurannya adalah 260 MB. Lalu masuk ke cmd sebagai administrator (run as administrator). Sekarang ketik perintah
“diskpart’ untuk menjalankan diskpart. Sekarang ketik perintah “list disk” untuk mengidentifikasi partisi efi.
Sekarang ketik perintah  “select disk 0”, ini tergantung dengan komputer kamu di kasusku efi berada di disk 0,
cara mengetahuinya silahkan lihat pada bagian disk management tadi.

![](/posts/20240312/1-tampilan-cmd.png)

Kemudian ketik perintah “list partition” dan identifikasi mana partisi efi itu tipsnya ingat ukurannyan tadi dalam kasusku
adalah 260MB dan dia berada di partisi 1 karena dia di partisi 1, aku mengetik perintah “select partition 1”. Setelah
mengetik perintah itu ketik perinath “assign letter=x” (untuk hurufnya boleh apa saja selain x). Kemudian masih di cmd
tadi, sekarang ketik perintah “exit” untuk menutup diskpart. Kemudian ketik “ x:” (sesuai dengan letter yang kamu assign tadi),
setelah kamu menekan enter. Sekarang ketik perintah “dir” untuk menampilkan folder dan file di x tadi, setelah terlihat
ada folder efi. Sekarang ketik “cd efi” dan ketik “dir” untuk menampilkan folder dan file pada folder efi.

Setelah kamu mengetik perintah “dir” tadi selanjutnya kamu akan melihat beberapa folder diantaranya ada Ubuntu dalam
kasuskku karena aku menginstall Ubuntu sebelumnya. Nah, itu folder yang akan kita hapus, untuk menghapusnya sekarang
silahkan ketik perintah “rmdir ubuntu /s”. Jika muncul dialog ketik saja “Y” lalu enter.

Setelah ini silahkan reboot ulang, dan masuk ke bios dan lihat sekarang menu boot untuk Ubuntu sudah hilang dan masalah
terselesaikan, dan itulah langkah-langkah untuk menghapus Ubuntu dari boot menu, semoga membantu.
