# Dockerized NodeJS Application

Untuk sesi ini kita mencoba untuk membuat Docker image untuk aplikasi NodeJS. NodeJS ini sering digunakan untuk membuat aplikasi backend atau RESTful API. Pada skenario kita akan membuat Docker Image untuk aplikasi NodeJS sederhana.

### Understand the contents of the Dockerfile

Pada syntax Dockerfile disini terdapat beberapa syntax baru yang ada pada step sebelumnya. Berikut adalah penjelasannya:

- `RUN chown node:node /app` : disini syntax RUN berfungsi untuk menjalankan perintah linux, yang mana disini akan menjalankan chown node:node /app yang mana command ini memiliki arti mengubah kepemilikan direktori /app menjadi milik user node dan grup node.

- `RUN apk update && apk add tzdata --no-cache` : syntax ini mengupdate package dari alpine dan menginstall tzdata untuk mengatur timezone pada container.

- `ENV TZ=Asia/Jakarta` : syntax ini berfungsi untuk mendefinisikan environment variable dan menanamkan didalam system container, dan bisa digunakan untuk mengatur timezone menjadi Waktu Indonesia Barat.

- `USER node` : syntax ini digunakan untuk user default yang digunakan oleh container, secara default container menggunakan user root, dan itu kurang _best practice_.

- `CMD [ "node", "./bin/www" ]` : syntax ini digunakan sebagai default command saat container startup, jadi saat container dijalankan secara otomatis akan menjalankan command `node ./bin/www` yang mana command tersebut untuk menjalankan aplikasi.

### How to use

untuk sesi ini bisa kita langsung execute untuk build dan run dengan perintah berikut:

```docker build -t my-nodejs-app .```

```docker run -dp 3000:3000 --name my-nodejs-app my-nodejs-app```

setelah coba buka browser dan akses http://localhost:3000, jika muncul website yang kita buat maka project sudah berhasil.

Selanjutnya kita coba push image yang sudah kita buat ini ke container registry, yang mana kita akan menggunakan Docker Hub. Pastikan kalian sudah memiliki akun Docker Hub dan sudah login Docker Hub di local development kalian. Berikut command untuk push ke registry:

```docker tag my-web pisckitama/my-nodejs-app```

```docker push pisckitama/my-nodejs-app```

Lalu coba cek ke Docker Hub dan seharusnya image dengan nama my-nodejs-app sudah muncul.

### Finish Chapter

Silahkan lanjut ke Project Berikutnya: [Docker Multistage Build](https://github.com/pisckipratama/docker-notes/tree/main/4-multistage-build-docker)