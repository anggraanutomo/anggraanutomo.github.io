---
title: Web 101 Bagian 4 - Mempersiapkan Web Server Nginx
date: 2022-10-29 20:17:00 +0700
categories: [Blogging, Tutorial]
tags: [Nginx, ufw, http]
---

## Ikhtisar
Sampai tahap ini, kita harus memiliki nama domain dan server, dan nama domain
harus diarahkan ke alamat IP server melalui DNS record. Sebagaimana yang saya
katakan di postingan sebelumnya, dalam seri tulisan ini instruksi yang akan
saya buat adalah untuk Debian, distribusi linux lain mungkin bisa menyesuaikan.

## Masuk ke server
Pertama, kita ingin masuk ke server VPS kita agar mendapatkan akses melalui terminal
bash di mana kita bisa mengatur server web. Disini aku mengasumsikan kamu memakai linux
atau MacOs dan tahu caranya membuka terminal. Untuk di Windows, kamu juga bisa menggunkan
PuTTY atau bisa seperti aku, yang menggunakan Windows Subsytem for Linux.

Sekarang buka terminal di komputer lokalmu, dan ketik

```bash
ssh root@namadomainmu.org
```

Perintah ini akan melakukan koneksi login ke server. Kemudian akan muncul sebuah prompt
menyuruh kamu untuk memasukkan password, kamu bisa memasukkan password yang sudah kamu buat
sebelumnya di DigitalOcean saat pembuatan droplet.

Kalau kamu mengalami error, mungkin terdapat masalah di dalam DNS record. Coba cek
lagi di bagian management dns. Sebagai tips kamu juga bisa mengganti `namadomainmu.org`
dengan alamat IP servermu, tapi kalau bisa diusahakan pakai nama domain, segera perbaiki
management dns mu.

## Menginstall Webserver Nginx
Kalau kamu tidak mengalami error, sekarang kamu sudah masuk ke dalam server menggunakan program
ssh. Mari kita mulai mengupdate, mengupgrade dan menginstall nginx, ketikan perintah berikut di terminal

```bash
apt update
apt upgrade
apt install nginx
```

Perintah pertama mengecek apakah ada package yang bisa diupdate, dan perintah yang kedua menginstall
package yang bisa diupdate.

Perintah ketiga adalah untuk menginstall nginx (dibaca Engine-X) yang mana webserver yang akan kita gunakan,
beserta dependensi-dependensi yang dibutuhkan nginx.

### Konfigurasi nginx
Nginx adalah webservermu. Kamu bisa membuat situs web, kemudian copy ke VPSmu, lalu beritahu nginx
di mana letaknya dan nginx akan menghost situs webmu tadi. Sangat simpel, mari kita buat konfigurasinya.

File konfigurasi nginx ada di `/etc/nginx`{: .filepath}. Ada dua subdirektori utama di sana (mungkin turunan Debian seperti
Ubuntu juga sama) yaitu `/etc/nginx/sites-available`{: .filepath } dan `/etc/nginx/sites-enabled`{: .filepath}.
Namanya sudah cukup deskriptif, secara sederhananya kamu bisa membuat
file konfigurasi di sites-available dan ketika sudah siap, kamu bisa membuat
*linking* ke sites-enabled yang akan mengaktifkan konfigurasi tadi.

Pertama, mari kita buat pengaturan untuk situs web kita. Kamu bisa copas
dan rubah sesuai kebutuhan, aku juga akan menjelaskan apa yang dilakukan baris-baris
tersebut.

Buat sebuah file di `etc/nginx/sites-available`{: .filepath }.

```bash
vi /etc/nginx/sites-available/webku
```

Perhatikan bahwa `vi` adalah teks editor di command line. Dengan begitu sekarang kamu bisa membuat dan mengedit file tersebut.
Perhatikan juga disitu saya membuat nama filenya webku, kamu bisa menggantinya terserah dengan nama yang kamu suka.

Aku akan menambahkan isi konten berikut ke dalam file tadi

```nginx
server {
        listen 80 ;
        listen [::]:80 ;
        server_name example.org ;
        root /var/www/webku ;
        index index.html index.htm index.nginx-debian.html ;
        location / {
                try_files $uri $uri/ =404 ;
        }
}
```
#### Penjelasan
Baris `listen` menyuruh nginx untuk mendengarkan koneksi dari IPv4 dan IPv6

`server_name` adalah nama server yang akan ditunjuk oleh konfigurasi ini. Contohnya dengan memasukkan ang.my.id di sini, berarti setiap
kali seseorang menghubungkan ke server ini dan mencari alamat tersebut, mereka akan diarahkan ke konten yang ada
di dalam blok ini.

`root` menentukan direktori di mana kita akan meletakkan file situs web kita. Secara teoritis ini bisa di mana saja,
tapi umumnya diletakkan di `/var/www`{: .filepath}. Silahkan disitu beri nama direktori yang kamu inginkan

`index` menentukan apa yang menjadi default. Biasanya saat kamu pergi ke suatu situs web, misalnya ang.my.id maka kamu
sebenarnya akan menuju ke file ang.my.id/index.html.

Terakhir `location` memberi tahu server bagaimana cara mencari file yang diminta oleh pengunjung situs. "location"
menentukan lokasi file yang dicari, dalam contoh ini, lokasinya adalah root
atau "/". Kemudian, perintah "try_files" akan mencoba mencari file yang diminta
dengan URI yang diberikan ($uri) dan jika file tersebut tidak ditemukan, akan
mencoba mencari file dengan URI yang diikuti tanda "/" ($uri/). Jika kedua file
tersebut juga tidak ditemukan, maka akan dikembalikan kode eror 404("=404").


## Membuat direktori dan index situs
Mari kita membuat sebuah halaman situs sederhana yang akan muncul saat seseorang
mencari domain tersebut.

```bash
mkdir /var/www/webku
```

Sekarang mari kita buat file index di dalam direktori tersebut
yang nantinya akan muncul saat situs web diakses:

```bash
vi /var/www/webku/index.html
```

Aku akan menambahkan halaman dasar html, kamu bisa menambahkannya sesuai dengan
selera kamu. file html inilah nanti yang akan muncul, saat seseorang mengakses
webmu.

```html
<!DOCTYPE html>
<h1>Websiteku</h1>
<p>Selamat datang di website aku, terimkasih telah berkunjung</p>
<p>Sekarang website ini bisa diakses melalui internet</p>
```

## Linking ke sites-enabled
Setelah kamu menyimpan file tersebut, kita dapat mengaktifkannya dengan
membuat link ke direktori `sites-enabled`.

```bash
ln -s /etc/nginx/sites-available/webku /etc/nginx/sites-enabled
```

Sekarang kita dapat melakukan reload atau restart, agar nginx melayani konfigurasi
yang telah kita buat

```bash
systemctl reload nginx
```

## Firewall
Pertama-tama install terlebih dahulu prograf `ufw`, `ufw` merupakan sebuah prograf
firewall dengan mengetikkan perintah

```bash
apt install ufw
```

Kita harus membuka port 80 dan port 443 seperti perintah di bawah:

```bash
ufw allow 80
ufw allow 443
```

Port 80 merupakan port bawaan untuk webserver, sedangkan 443 merupakan port
yang digunakan untuk koneksi yang terenkripsi.


## Panduan keamanan
Secara default, nginx dan web server lain secara otomatis akan menampilkan
nomor versi mereka di halaman eror. Sangat disarankan untuk menghide nomor versi
tersebut, karena seseorang bisa saja menemukan suatu exploit di nginx versi
tertentu dan bisa saja mengexploit webserver punyamu, oleh karena itu hide
versi nginx mu. Edit file `/etc/nginx/nginx.conf`{: .filepath}, dan temukan
baris `# server_tokens off;`. hapus tanda pagar, dan reload nginx.

Pastikan webserver kamu selalu up to date untuk mendapatkan pembaruan security terbaru.

## Sekarang web kamu sudah jalan
Pada saat ini , kamu sekarang bisa mengetikan alamat situs web kamu di browser,
dan halaman web ini akan muncul!

![halaman web](/posts/20221029/1-live.png)

Perhatikan ada tulisan `Not secure` di notifikasi. Postingan selanjutnya
akan memberikan langkah-langkah bagaimana mengenkripsi koneksi ke web kamu.
