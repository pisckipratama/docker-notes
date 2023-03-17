# Docker Multistage Build

Multi Stage Docker build adalah metode pengorganisasian Dockerfile untuk meminimalkan ukuran container akhir dengan pengaturan perintah dan Dockerfile yang lebih baik. Dari metode tersebut akan menyediakan eksekusi standar untuk menjalankan tindakan build. Untuk lebih lanjutnya dapat anda lihat [di link berikut](https://docs.docker.com/build/building/multi-stage/).

Referensi: [Menggunakan Multi-Stage Docker Builds di Rust](https://abdanmulia.medium.com/menggunakan-multi-stage-docker-builds-di-rust-b04d3e38c665)

# Why Multistage Build?

Docker Container biasanya dibuat dengan menggunakan Dockerfile. Dalam file tersebut berisi sekumpulan instruksi untuk menginstal dependensi, compile source code, kemudian build aplikasi. Namun, seringkali hal-hal yang diperlukan untuk build aplikasi bukanlah hal yang diperlukan untuk menjalankan aplikasi yang kita kembangkan.

### Understand the contents of the Dockerfile

Pada syntax Dockerfile disini terdapat beberapa syntax baru yang ada pada step sebelumnya. Berikut adalah penjelasannya:

- `FROM node:16-slim AS build` : dalam syntax FROM ada tambahan syntax AS yang mana ini berfungsi sebagai mendefisinikan stage, yang mana disini menggunakan nama build sebagai stagenya.

### How to use

untuk sesi ini bisa kita langsung execute untuk build dan run dengan perintah berikut:

```docker build -t my-react-app .```

Jika ingin membuild hanya pada stage tertentu saja bisa menggunakan perintah:

```docker build -t my-react-app --target build .```

Untuk menjalankan container bisa menggunakan perintah

```docker run -dp 80:80 --name my-react-app my-react-app```

setelah coba buka browser dan akses http://localhost, jika muncul website yang kita buat maka project sudah berhasil.

Selanjutnya kita coba push image yang sudah kita buat ini ke container registry, yang mana kita akan menggunakan Docker Hub. Pastikan kalian sudah memiliki akun Docker Hub dan sudah login Docker Hub di local development kalian. Berikut command untuk push ke registry:

```docker tag my-react-app pisckitama/my-react-app```

```docker push pisckitama/my-react-app```

Lalu coba cek ke Docker Hub dan seharusnya image dengan nama my-react-app sudah muncul.

### Finish Chapter

Silahkan lanjut ke Project Berikutnya: [Docker Compose](https://github.com/pisckipratama/docker-notes/tree/main/5-docker-compose)