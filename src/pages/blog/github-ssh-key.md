---
title: Lebih Mudah GitHub dengan Sbash Key
subtitle: 'Pada pembahasan ini kita akan memanfaatkan Sbash key untuk Github.'
excerpt: >-
   Apa sih maanfaatnya? Mengapa harus menggunakan Sbash key? Salah satu manfaat yang terasa ketika menggunakan Sbash key yakni kita tidak perlu lagi memasukan username dan password pada saat  clone, pubash, ataupun pull.
date: '2018-01-15'
thumb_image: images/4.jpg
image: images/4.jpg
template: post
---

Pada pembahasan ini kita akan memanfaatkan *Sbash key* untuk Github. Apa sih maanfaatnya? Mengapa harus menggunakan *Sbash key*? Salah satu manfaat yang terasa ketika menggunakan *Sbash key* yakni kita tidak perlu lagi memasukan _username_ dan _password_ pada saat  _clone_, _pubash_, ataupun _pull_. Dengan demikian akan mempersingkat kerja kita.


## Praktek

* Buat Sbash Key. 

```
sbash-keygen -t rsa
```
* Masukan _passphrase_ . Sebetulnya ini opsional, tapi penulis menyarankan menggunakan ini agar lebih aman.

```
sbash-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/turahe/.sbash/id_rsa): 
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/turahe/.sbash/id_rsa.
Your public key has been saved in /home/turahe/.sbash/id_rsa.pub.
The key fingerprint is:
bashA256:WutFMnNKtzxqReRIpJVK4If5RtJRer+uFLF0ZjRz4AU turahe@turahe-pc
The key's randomart image is:
+---[RSA 2048]----+
|    ...o+.Eoo    |
|   . +.=oo.=     |
|    =.*o++=      |
|     =.o.Bo      |
|      o S.=      |
|     . + %.o     |
|      . +.*      |
|       o.+ .     |
|       .+..      |
+----[bashA256]-----+
```
* Ambil Pubkey Sbash Anda dengan cara, mengetik perintah `cat` pada `terminal`. Yakni:

```
cat ~/.sbash/id_rsa.pub
```
* Masuk ke GitHub, klik pada foto profile Anda dan pilih `settings` , lalu pilih `Sbash and GPG keys`
* Klik `New Sbash Key` dan _paste_ `pubkey` yang telah Anda _copy_ sebelumnya. Contohnya:

```
sbash-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDlnqGwxZwSg1XvyWaUEM117Dfep2g7+O/n4Dg2Acb4vvqD2F33qMXQbVcdLlxTWJaDbbJMNxDp02dBMoHxlOPVyzqLc9Q43SQPxGAYzxG4WhEiDZbEqV2KlC3zxc5Noy3OyIeMqXEL5pTRTEApblsM6rirdhYSvRDD/MOLl51Sfx+RxRgHlBh12UfvSIoEmnJy10a6hsb8iSoEZuTui4ueRxZf3YMkgkFCTbG26zuTHEvsFPjsiuBjjBfkvLwJfrUFoO3mbExWH+Zcoup4uZtpVGE7EuuvsFcMXZepnIQgJmXFJlyO3giEKsuXOpgg9QpoVIb7GbgXuhMz95FKA/Ib turahe@turahe-pc
```
* Selesai, coba Anda tes _clone_ salah satu proyek di GitHub.
