---
title: Memasang MongoDB dan Mongo Express Melalui Docker
date: 2022-11-23 01:08:00 +0700
categories: [Blogging, Tutorial]
tags: [mongodb, mongo express, docker, yaml, compose]
---

## Docker Compose
Docker merupakan sebuah program yang menyederhanakan proses pengelolaan aplikasi
di dalam kontainer, sedikit mirip dengan *virtual machine*. Bedanya kontainer ini
lebih ringan dan ramah sumber daya. Dengan adanya Docker akan memudahkan *developer*
dalam membuat lingkungan aplikasi yang terisolasi dari komputer utama.

Dalam sebagian kasus terdapat aplikasi yang bergantung dengan aplikasi lain, sehingga
untuk mengatur kontainer dari tiap aplikasi agar dapat memulai, berkomunikasi, dan menutup
secara bersamaan akan menjadi hal yang sulit.

Dengan Docker Compose, developer dapat menggunakan ini untuk membangun lingkungan
aplikasi multi-kontainer sesuai dengan definisi yang telah ditetapkan dalam file
YAML. Sehingga berkat adanya Docker Compose ini kontainer-kontainer tadi dapat berbagi
volume penyimpanan dan jaringan yang sama.

## MongoDB dan Mongo Express
Untuk membuat lingkungan MongoDB dan Mongo Express, buat file baru bernama `docker-compose.yaml`.
Kemudian isi file tersebut dengan skrip berikut :

```yaml
version: "3.8"
services:
  mongodb:
    image: mongo:4.4.5
    container_name: mongodb
    ports:
      - 27017:27017
    volumes:
      - data:/data
    environment:
      - MONGO_INITDB_ROOT_USERNAME=rootuser
      - MONGO_INITDB_ROOT_PASSWORD=rootpass
  mongo-express:
    image: mongo-express:0.54.0
    container_name: mongo_express
    restart: always
    ports:
      - 8081:8081
    environment:
      - ME_CONFIG_MONGODB_ADMINUSERNAME=rootuser
      - ME_CONFIG_MONGODB_ADMINPASSWORD=rootpass
      - ME_CONFIG_MONGODB_SERVER=mongodb
volumes:
  data: {}

networks:
  default:
    name: mongodb_network
```

Kemudian ketik perintah `docker-compose -f docker-compose.yaml up` atau `docker compose up` di terminal agar docker
menjalankan aplikasi yang telah didefinisikan di `docker-compose.yaml` tadi. Kalau imagenya belum ada di
komputer maka akan di pull terlebih dahulu. Untuk menghapus semua data di aplikasi kontainer tersebut dapat memasukkan
perintah `docker compose down`. Menjalankan docker compose lewat background atau mode detach dapat memasukkan perintah
`docker compose up -d`

![mongo express](/posts/20221123/01-mongo-express.png)

Jika service sudah berjalan, silahkan mengunjungi [localhost:8081](http://localhost:8081) maka akan terlihat halaman Mongo Express.

## Menghubungkan MongoDB Shell ke Database
Untuk mengakses database di MongoDB dapat menggunakan GUI Client seperti Mongo Express diatas. Selain itu juga dapat
menggunakan Mongo Shell. Perintah untuk melakukan koneksi ke database menggunakan Mongo Shell adalah
`mongo mongodb://localhost:27017 -u rootuser -p rootpass`

Kemudian untuk menggunakan Mongo Shell terlebih dahulu kita harus mengetahui container id dari mongo image tersebut.
Caranya adalah ketikan perintah `docker ps` nanti akan muncul process image apa saja yang sedang berjalan. Seperti gambar
di bawah

![docker ps](/posts/20221123/02-docker-ps.png)

Pada gambar di atas container id dari image mongo adalah `e920b8e5b424`. Setelah mengetahui container id-nya maka
ketikan perintah `docker exec -it e920b8e5b424 bash` agar masuk ke container tersebut menggunakan shell bash.

![masuk ke container](/posts/20221123/03-masuk-ke-kontainer.png)

Barulah setelah itu mengetikan perintah untuk melakukan koneksi ke database yaitu
`mongo mongodb://localhost:27017 -u rootuser -p rootpass` maka akan masuk ke Mongo Shell

![masuk ke mongoshell](/posts/20221123/04-masuk-ke-mongosh.png)

Setelah masuk ke Mongo Shell maka kita dapat melakukan query-query ke database MongoDB tersebut. Contohnya adalah
menampilkan semua database yang ada di kontainer dapat memasukkan perintah `show dbs;`

![show dbs](/posts/20221123/05-show-dbs.png)

Pada Mongo Shell untuk membersihkan layar dapat menekan tombol <kbd>CTRL</kbd> + <kbd>L</kbd>
