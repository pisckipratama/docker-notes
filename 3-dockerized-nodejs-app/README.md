# Dockerized NodeJS Application

Untuk sesi ini kita mencoba untuk membuat Docker image untuk website static atau yang sering digunakan sebagai _landing page_. Di skenario ini sudah ada contoh source code native website (html, css, js). Kita akan menggunakan NGINX sebagai base image, lalu copy semua file yang ada pada folder ke default directory NGINX yang dijadikan sebagai index webserver yaitu /usr/share/nginx/html.

### Understand the contents of the Dockerfile

Pada syntax Dockerfile disini terdapat beberapa syntax baru yang ada pada step sebelumnya. Berikut adalah penjelasannya:

- `LABEL="Piscki F. Pratama <pisckipratama@gmail.com>"` : yang berarti ini mendeskripsikan atau memberikan informasi untuk Docker image yang kita buat. Label ini bersifat key value yang mana dicontoh ini kita mendefinisikan `maintainer="Piscki Pratama <pisckipratama@gmail.com>"` yang berarti key-nya adalah `maintainer` lalu value-nya `"Piscki Pratama <pisckipratama@gmail.com>"`. Fungsi disini berarti memberi deskripsi kontak dari maintainer atau administratornya.

- `COPY . /usr/share/nginx/html` : syntax ini untuk menyalin semua file yang ada di folder saat ini diakses ke folder `/usr/share/nginx/html` yang mana folder tersebut digunakan sebagai index default untuk web server.

- `EXPOSE 80` : syntax ini digunakan untuk mengexpose port, port yang diexpose disini adalah port 80.

### How to use

untuk sesi ini bisa kita langsung execute untuk build dan run dengan perintah berikut:

```docker build -t my-web .```

```docker run -dp 4000:80 --name my-web my-web```

setelah coba buka browser dan akses http://localhost:4000, jika muncul website yang kita buat maka project sudah berhasil.

Selanjutnya kita coba push image yang sudah kita buat ini ke container registry, yang mana kita akan menggunakan Docker Hub. Pastikan kalian sudah memiliki akun Docker Hub.

Untuk melakukan push docker image kita harus mendefinisikan username Docker Hub yang kita miliki, misal disini saya mempunyai akun Docker Hub dengan username `pisckitama` berarti saya perlu mendefinisikan tag atau nama image nya sebagai berikut: `pisckitama/my-web`. kita tidak perlu lagi melakukan build dengan tag seperti itu, kita bisa menggunakan fitur `tag` dari Docker, berikut perintahnya:

```docker tag my-web pisckitama/my-web```

Sebelum melakukan push, kita juga perlu login ke akun Docker Hub kita di Docker yang terinstall di local. Perintah untuk login ke Docker Hub bisa menggunakan:

```docker login```

lalu masukkan username dan password. Setelah itu coba untuk push image dengan perintah: 

```docker push pisckitama/my-web```

Lalu coba cek ke Docker Hub dan seharusnya image dengan nama my-web sudah muncul.

### Finish Chapter

Silahkan lanjut ke Project Berikutnya: [Docker Multistage Build](https://github.com/pisckipratama/docker-notes/tree/main/4-multistage-build-docker)