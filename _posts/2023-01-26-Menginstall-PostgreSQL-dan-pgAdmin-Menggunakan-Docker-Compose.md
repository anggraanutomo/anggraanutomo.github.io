---
title: Menginstall PostgreSQL dan pgAdmin Menggunakan Docker Compose
date: 2023-01-26 09:01:00 +0700
categories: [Panduan]
tags: [PostgreSQL, pgAdmin, Docker, Docker Compose, Database, Installation, Configuration, DevOps, Containerization]
---

Jadi beberapa waktu yang lalu, aku menemukan diriku dalam situasi dimana aku harus menginstall PostgreSQL dan pgAdmin
secara lokal untuk proyek pribadi yang sedang kukerjakan. Berangkat dari pengalamanku sukses menginstall [MongoDB dan
Mongo Express secara lokal](https://anggra.id/posts/Membuat-Docker-Compose-MongoDB-dan-MongoExpress/){:target="_blank"}
, maka sebaiknya aku akan menginstall ini menggunakan docker saja.

Dalam artikel singkat ini, aku akan menjelaskan bagaimana proses-proses penginstallan PostgreSQL dan pgAdmin menggunakan
Docker Compose. Sebelum itu mungkin secara singkat aku akan menjelaskan apa itu PostgreSQL dan pgAdmin terlebih dahulu.

Secara singkatnya, PostgreSQL merupakan sebuah sistem manajemen basis data relasional open-source, sedangkan pgAdmin
merupakan aplikasi open-source yang digunakan untuk mengelola dan mengakses basis data PostgreSQL yang berbasis GUI dan
dapat diakses di browser. 😃

## Menginstall PostgreSQL dan pgAdmin
Buat file baru bernama `docker-compose.yml` kemudian isi file tersebut dengan script sebagai berikut

```yml
version: '3'
services:
  db:
    image: postgres:bullseye
    container_name: postgresdb
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=password
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - my-network
  pgadmin4:
    image: dpage/pgadmin4
    container_name: pgadmin4
    environment:
      - PGADMIN_DEFAULT_EMAIL=halo@anggra.id
      - PGADMIN_DEFAULT_PASSWORD=password
    ports:
      - "5050:80"
    networks:
      - my-network

volumes:
  pgdata:

networks:
  my-network:
```

Kemudian seperti biasa ketikkan perintah `docker-compose -f docker-compose.yml up` atau `docker compose up` agar docker
mempull image yang telah didefiniskan diatas kalau image tersebut belum ada di lokal. Untuk menghapus semua data di
kontainer tersebut dapat memasukkan perintah `docker compose down`, menjalankan docker compose sebagai background
dapat memasukkan perintah `docker compose up -d`


## Menghubungkan pgAdmin ke server PostgreSQL
Kalau servicenya sudah berjalan silahkan kunjungi [localhost:5050](http://localhost:5050){:target="_blank"} maka akan
muncul tampilan seperti, berikut

![tampilan_login_pgadmin](/posts/20230126/01-tampilanloginpgadmin.png)

Kemudian masukkan email address dan password, untuk menemukan email dan password silahkan lihat kembali berkas
`docker-compose.yml` maka disitu ditemukan bahwa default email dan password adalah `halo@anggra.id` dan `password`
setelah itu klik login, maka akan masuk ke halaman dashboard.

![koneksi_ke_database](/posts/20230126/02-registerserverdatabase.png)

Untuk menghubungkan ke server database klik kanan pada `Servers` kemudian pilih `Register` lalu `Server...` seperti
gambar diatas.

Kemudian pada tab `General` namanya terserah contohnya bisa dikasih nama __postgres__, kemudian pada tab `Connection`
pada input `Hostname/address` masukkan `postgresdb`, `Username` masukan `postgres` dan `Password` masukkan `password`
kemudian klik `Save`

![konfigurasi](/posts/20230126/03-konfigurasi.png)

Setelah konfigurasi selesai dan kamu tekan `Save` maka akan muncul tampilan seperti berikut yang menandakan kamu
telah berhasil menghubungkan pgAdmin dengan server database postgre tersebut.

![berhasil](/posts/20230126/04-berhasil.png)
