# docker-compose-laravel

Adalah template docker-compose simple yang dimodifikasi dari [aschmelyun/docker-compose-laravel](https://github.com/aschmelyun/docker-compose-laravel), dimana saya menghapus service mysql karena tidak diperlukan

## Penggunaan

1. Untuk memulai, pastikan anda memiliki [Docker terinstall](https://docs.docker.com/docker-for-mac/install/), dan clone repo ini
1. (opsional), ganti nama `site`, terserah anda.
1. Selanjutnya, navigasi ke root folder template docker dan nyalakan container dengan menjalankan `docker-compose up -d --build {site atau nama yang sudah diganti}`
1. Masukkan situs laravel anda ke `/src` atau jalankan `docker-compose run --rm composer create-project laravel/laravel`

## Pengunaan dengan NGINX Proxy manager
Pada bagian `site`, hapus deklarasi `port` untuk menutup port 80. ini memastikan apabila anda menjalankan lebih dari 1 kontainer, port tidak akan konflik. lalu, sambungkan network `site` ke NGINX proxy manager. setelah itu, tambahkan proxy pass ke `{site / nama kontainer anda}` dengan port 80

Menyalakan jaringan Docker Compose dengan `site` alih-alih hanya menggunakan `up`, memastikan bahwa hanya container ini yang dinyalakan, bukan semua container yang ada. Berikut adalah port yang terekspos di instance ini:

- **nginx** - `:80` (bila terbuka)
- **php** - `:9000`

Tiga kontainer tambahan disertakan yang menangani perintah Composer, NPM, dan Artisan * tanpa * harus menginstal alat ini di komputer lokal Anda. Gunakan contoh perintah berikut di root proyek Anda, modifikasi agar sesuai dengan kasus penggunaan khusus Anda.

- `docker-compose run --rm composer update`
- `docker-compose run --rm npm run dev`
- `docker-compose run --rm artisan migrate` 
