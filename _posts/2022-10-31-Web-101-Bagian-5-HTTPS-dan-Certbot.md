---
title: Web 101 Bagian 5 - HTTPS dan Certbot
date: 2022-10-31 14:31:10 +0700
categories: [Blogging, Tutorial]
tags: [https, certbot, encryption, tls]
---

## Ikhtisar
Sebagian besar orang tidak menyadari betapa pentingnya mengenkripsi koneksi saat mengakses suatu situs web.
Melalui HTTPS/SSL, informasi yang dikirimkan antara komputer kamu dan webserver terlindungi dari pihak-pihak yang
tidak bertanggung jawab yang mungkin mencoba mengintai atau mencuri informasi yang dikirimkan.

Certbot adalah program yang membuat dan mengelola sertifikat yang memungkinkan koneksi untuk terenkripsi. Sebelumnya,
membuat sertifikat seringkali merupakan proses yang sulit dan mahal, namun dengan adanya Certbot, proses tersebut
menjadi lebih mudah dan gratis. Dengan menggunakan Certbot, kamu dapat dengan mudah membuat sertifikat yang valid
untuk situs web kamu, yang kemudian dapat digunakan untuk mengenkripsi koneksi melalui HTTP/SSL.

## Kenapa enkripsi penting
- Dengan mengenkripsi koneksi melalui HTTPS/SSL, ISP tidak dapat menyadap apa yang dilihat oleh pengguna saat mengakses
webmu. Mereka tahu kamu terhubung, tetapi halaman yang dikunjungi, di enkripsi sehingga yang dilihat orang
ISP hanya campuran kata dan huruf yang tidak jelas.
- Mesin pencari seperti Google lebih menyukai halaman dengan HTTPS dari pada HTTP yang tidak terenkripsi
- Situs web kamu akan mendapat gembok kunci berwarna hijau di sebelah address bar, sehingga
membuat orang percaya web kamu aman.

## Mari mengenkripsi

![belum terenkripsi](/posts/20221029/1-live.png)

Terlihat pada gambar diatas, saat web browser mengakses web kamu muncul tulisan
"Not secure" yang memeberitahu pengunjung bahwa web kamu tidak terenkripsi.

## Instalasi

Silahkan jalankan :

```bash
apt install python3-certbot-nginx
```

Ini akan menginstall certbot dan modul untuk nginx


## Jalankan
Seperti yang sudah dijelaskan di postingan sebelumnya, firewall mungkin
akan bentrok dengan certbot. Jadi solusinya adalah kamu bisa mematikan firewall
atau membolehkan koneksi di port 80 dan 443 :

```bash
ufw allow 80
ufw allow 443
```

Kemudian jalankan certbot:

```bash
certbot --nginx
```

Dengan perintah tersebut, kamu dapat mengatur sertifikat yang akan diperbarui secara otomatis.
Nanti kamu disuruh untuk memberikan alamat emailmu agar dapat mengirimkan pemberitahuan saat sertifikat
perlu diperbarui. Jika kamu tidak ingin memberikan email, kamu dapat menggunakan opsi --register-unsafely-without-email

Setelah itu silahkan menekan y dan enter jika disuruh menyetujui layanan dan ketentuan

Setelah selesai, certbot akan menanyakan ke kamu domain mana yang ingin diberi sertifikat ssl, kamu bisa menekan
enter untuk memilih semua.

![certbot](/posts/20221029/3-certbot.png)

Dibutuhkan beberapa waktu untuk membuat sertifikat, setelah itu akan muncul tulisan congratulation

![certbot](/posts/20221029/4-congrats.png)

Jika muncul tulisan seperti itu selamat, sekarang web kamu sudah terenkripsi.

## Mengecek HTTPS
Sekarang silahkan kunjungi web kamu dan perhatikan sekarang muncul, gambar gembok
dan tulisan "Not secure" sudah hilang, yang menandakan kamu sudah berhasil
mengenkripsi website kamu.

![ssl](/posts/20221029/2-ssl.png)

## Menyetting pembaruan sertifikat otomatis
Sebagaimana yang telah ku bilang sebelumnya, sertifkat Certbot hanya berlaku
selama 3 bulan. Untuk memperbarui, kamu hanya perlu menjalankan pertintah
`certbot --nginx renew`. Untuk memastikan bahwa sertifikat diperbarui secara otomatis
kamu bisa mengatur `cronjob` untuk menjalankan perintah ini, cukup jalankan perintah berikut :

```bash
crontab -e
```

Akan muncul menu kamu ingin menggunakan teks editor apa untuk mengedit file tersebut,
silahkan pilih 1 jika kamu mengerti vi.

Setelah itu akan muncul teks editor beserta boilerplate awal file tersebut, untuk penjelasannya
crontab sendiri adalah sebuah file yang berisi daftar perintah yang akan dijalankan
secara otomatis pada waktu yang telah ditentukan. crontab biasanya digunakan untuk menjalakan perintah-
perintah kecil yang perlu dilakukan secara terjadwal, seperti menjalankan script backup, mengirim email,
atau menjalan perintah lain yang terjadwal. Pada kasus ini kita akan memberi tahu crontab
untuk secara otomatis mencoba memperbarui sertifikat kita setiap bulan sehingga kita tidak perlu
melakukannya secara manual.

Tambahkan line baru di akhir file dan masukkan konten ini:

```crontab
0 0 1 * * certbot --nginx renew
```

Simpan file dan keluar untuk mengaktifkan cronjob tersebut.

Selamat sekarang kamu sudah mempunyai website yang bisa diakses melaului internet. Kamu sekarang bisa menambahkan apa yang
kamu mau di web tersebut.
