---
title: SCP 101 - Dasar-Dasar Mengcopy File Ke Remote Machine
date: 2023-01-12 20:46:00 +0700
categories: [Panduan]
tags: [scp, linux, copy, server, remote-machine, local-machine]
---

Pada saat kamu mempunyai vps mungkin akan bertanya-tanya, bagaimana jika aku ingin mengcopy file dari local machine
ke remote server vps tersebut? Dalam sistem operasi Linux, salah satu perintah yang dapat kamu gunakan untuk untuk
mengcopy file adalah `scp` atau `Secure Copy Protocol`. `scp` merupakan perintah yang digunakan untuk mengcopy file dari
satu komputer ke komputer lain dengan aman menggunakan enkripsi SSH.

## Mengcopy file dari local machine ke remote machine
Dalam proses mengcopy file dari local machine ke remote machine, kita akan menggunakan
perintah `scp` dengan sintaks sebagai berikut

```console
scp path/to/local/file user@remote_IP:remote_destination
```

atau

```console
scp path/to/local/file user@remote_hostname:remote_destination
```

Di mana "user" adalah nama pengguna yang digunakan untuk masuk ke remote machine,
"remote_IP" adalah alamat IP remote machine, "remote_hostname" adalah nama
host dari remote machine, dan "remote_destination" adalah lokasi tempat file akan
dicopy di remote machine

Opsi yang sering digunakan pada saat mengcopy file dari local machine ke remote machine
adalah `-r` yang digunakan untuk mengcopy direktori secara rekursif dan `-P` yang
digunakan untuk menentnukan port yang digunakan pada saat mengcopy file.

Contoh perintah yang digunakan untuk mengcopy file dari local machine ke remote machine adalah:

```console
scp /home/localuser/file.txt user@192.168.1.100:/home/remoteuser/
```

Perintah diatas akan mengcopy file `file.txt` yang berada di `/home/localuser/`{: .filepath } di local machine
ke lokasi `/home/remoteuser/`{: .filepath } di remote machine dengan IP 192.168.1.100

Selain itu, kita juga bisa mengcopy file dari local ke remote dengan spesifikasi
port yang berbeda dari port default yang digunakan scp yaitu 22. Contoh :

```console
scp -P 2222 /home/localuser/file.txt user@192.168.1.100:/home/remoteuser/
```

## Mengcopy file dari remote machine ke local machine
Kemudian untuk proses mengcopy file dari remote machine ke local machine,
kita dapat menggunakan perintah `scp` dengan sintaks sebagai berikut:

```console
scp user@remote_IP:path/to/remote/file local_destination
```

atau

```console
scp user@remote_hostname:path/to/remote/file local_destination
```

Contoh perintah yang digunakan untuk mengcopy file dari remote machine ke local
machine adalah:

```console
scp -r user@192.168.1.100:/home/user/file.txt /home/localuser/
```

Perintah diatas akan mengcopy file `file.txt` yang berada di `/home/user/`{: .filepath} dari remote
machine dengan IP 192.168.1.100 ke lokasi `/home/localuser/`{: .filepath } di local machine.

## Referensi
[https://linux.die.net/man/1/scp](https://linux.die.net/man/1/scp)

[https://www.ssh.com/academy/ssh/scp](https://www.ssh.com/academy/ssh/scp)
