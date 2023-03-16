# Dockerize Local Development Environment

Pada sesi ini kita akan mencoba membuat environment dev untuk mengembangkan aplikasi. Untuk contoh case disini kita akan menggunakan NodeJS yang mana nantinya kita juga akan mencoba menjalankannya.

Tujuan dari sesi ini kita bisa memanfaatkan Docker untuk pengembangan aplikasi di local kita sebagai programmer, yang mana nantinya tidak lagi menginstall tools yang diperlukan untuk mengembangkan aplikasi tersebut di local kita.

### Understand the contents of the Dockerfile

Pada syntax Dockerfile disini terdapat beberapa penjelasan sebagai berikut:

- `FROM node:16-alpine` yang berarti ini mengambil image nodejs dari Docker Hub dengan tag 16-alpine yang berarti versi 16 dengan system alpine. pada syntax sering dibilang juga sebagai _base image_.

- `WORKDIR /work` syntax WORKDIR disini berarti mendefinisikan direktori default dari image yang akan kita build `/work` disini berarti file location yang akan dijadikan default direktorinya, berarti disini kita mendefinisikan default direktori di `/work`.

### How to use it

Setelah memahami isi dari Dockerfile kita akan mencoba untuk membuild Dockerfile tersebut yang mana nantinya akan menjadi image yang akan kita gunakan untuk development aplikasi.

untuk build docker image bisa digunakan perintah berikut

```docker build -t <name> .```

sebagai contoh kita akan build dengan perintah berikut:

```docker build -t my-nodejs-dev .```

Setelah build coba lihat apakah muncul image yang sudah dibuat dengan perintah ```docker images```.

Lalu kita coba jalankan image tersebut dengan perintah:
```docker run -it -v ${PWD}:/work my-nodejs-dev sh```

- flag `-it` digunakan untuk menggunakan interactive tty sebagaimana fungsi untuk exec container.
- flag `-v ${PWD}:/work` digunakan untuk mounting volume lokasi direktori kita berada ke folder `/work` yang ada di container.
- `sh` berarti kita menjalankan command shell untuk menjalankan macam-macam perintah linux.