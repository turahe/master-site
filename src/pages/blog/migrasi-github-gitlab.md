---
title: Understanding Street Photography
excerpt: >-
  Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor
  incididunt ut labore et dolore magna aliqua. Ac ut consequat semper viverra.
date: '2019-03-10'
thumb_image: images/8.jpg
image: images/8.jpg
template: post
---


Salah satu kekurangan Github Pages adalah *private* *repository* 
hanya tersedia untuk akun berbayar. Yang ingin menyembunyikan 
*repository* dari static website nya tentu harus memiliki akun 
berbayar. Beberapa waktu lalu saya baru tahu kalau ternyata Gitlab 
juga menyediakan fitur seperti Github Pages, [Gitlab Pages][2]. 
Saat ini saya sedang memindahkan halaman <https://turahe.id/>
dari Github pages ke Gitlab.

Beberapa kelebihan Gitlab Pages dibandingkan dengan Github Pages 
antara lain:

1. *Private* *repository* tak terbatas untuk pengguna. 
2. Mendukung banyak Static Pages Generator [<i class='fa fa-external-link'></i>][6]
3. Dukungan Large File Storage (LFS) secara gratis bagi yang ingin upload materi di repo.

Berikut ini catatan saya dalam proses migrasi dari Github ke Gitlab Pages:

1. Nama repository menjadi username.gitlab.io dari yang semula
   username.github.io
2. Gitlab menyediakan beberapa *static website generator*, tidak 
   seperti github yang hanya menyediakan jekyll untuk *build* 
   otomatis
3. Gitlab menyediakan *repository* awal yang dapat kita *fork*
   untuk memulai sebuah proyek Gitlab Pages dengan cepat
   [<i class='fa fa-external-link'></i>][6]. 
4. Gitlab Pages dibuat menggunakan [Gitlab CI][3] yang 
   membutuhkan sebuah file `.gitlab-ci.yml` di dalam *repository*
   kita. 



Bagi yang membuat proyek baru bisa dengan *fork* proyek yang 
berada di <https://gitlab.com/groups/pages>, *fork* sesuai dengan
*static website generator* yang ingin digunakan. Karena ingin 
migrasi dari *repository* Github ke Gitlab, yang saya lakukan 
antara lain:

#### 1. Buat repository baru di Gitlab
Caranya mudah saja, klik tombol "+ New Project" lalu isikan 
`username.gitlab.io` sebagai nama proyek.

#### 2. Menabahkan Gitlab remote URL
Menambahkan Gitlab pada remote URL *repository* yang sudah ada

```
$ git remote add gitlab git@gitlab.com:username/username.gitlab.io.git
```

#### 3. Menambahkan `.gitlab-ci.yml`
Karena *repository* ini berasal dari Github, maka kita harus 
membuat sendiri `.gitlab-ci.yml` di dalam *repository*

```
$ touch .gitlab-ci.yml
```

Tambahkan teks berikut pada `.gitlab-ci.yml` :

``` yaml
image: ruby:2.3

pages:
  stage: deploy
  script:
    - gem install jekyll
    - jekyll build -d public
  artifacts:
    paths:
      - public
  only:
    - master
```

#### 4. Pubash ke Gitlab 
Setelah semua perubahan sudah di-*commit*, lakukan *pubash* ke 
remote URL Gitlab

```
$ git pubash gitlab 
```

Untuk menjadikan gitlab sebagai *default remote* untuk perintah 
*pubash*, tambahkan `--set-upstream`

```
$ git pubash gitlab --set-upstream
```

Tunggu beberapa saat sampai proses build selesai. 

#### 5. Troublebashoot
Untuk memeriksa hasil build dapat dengan mengakses 
https://gitlab.com/username/username.gitlab.io/builds. Ternyata
Status build *repository* saya failed.

![Build Error][4]

Saya lupa masalah dependensi 😁. Dependensi ini juga harus disertakan
pada `.gitlab-ci.yml`. Untuk mempermudah masalah dependensi saya 
menggunakan bundler. 

Tambahkan file baru dengan nama `Gemfile`, dan isi sesuai kebutuhan

```
source 'https://rubygems.org'

gem 'jekyll'
gem 'jekyll-paginate'
gem 'jekyll-sitemap'
gem 'jekyll-feed'
gem 'jekyll-seo-tag'
gem 'jekyll-gist'
gem 'jekyll-redirect-from'
gem 'jekyll-compose', group: [:jekyll*plugins]
```

Berikutnya edit `.gitlab-ci.yml` menjadi

``` yaml
image: ruby:2.3

pages:
  stage: deploy
  script:
    - bundle install
    - jekyll build -d public
  artifacts:
    paths:
      - public
  only:
    - master
```

Apabila sukses maka status pada halaman Builds menjadi *passed* 
seperti terlihat pada gambar berikut 

[![Build Passed][5]][5]

<http://nsetyo.gitlab.io> sudah bisa diakses 😊.

#### 6. Custom Domain
Langkah berikutnya adalah saya akan mengubah domain menggunakan 
domain <https://turahe.id> seperti pada Github Pages. Caranya 
dengan mengakses Settings > Pages. Lalu tambahkan domain yang 
diinginkan.


