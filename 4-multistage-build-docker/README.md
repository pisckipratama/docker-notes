# Docker Multistage Build

Multi Stage Docker build adalah metode pengorganisasian Dockerfile untuk meminimalkan ukuran container akhir dengan pengaturan perintah dan Dockerfile yang lebih baik. Dari metode tersebut akan menyediakan eksekusi standar untuk menjalankan tindakan build. Untuk lebih lanjutnya dapat anda lihat [di link berikut](https://docs.docker.com/build/building/multi-stage/).

Referensi: [Menggunakan Multi-Stage Docker Builds di Rust](https://abdanmulia.medium.com/menggunakan-multi-stage-docker-builds-di-rust-b04d3e38c665)

# Why Multistage Build?

Docker Container biasanya dibuat dengan menggunakan Dockerfile. Dalam file tersebut berisi sekumpulan instruksi untuk menginstal dependensi, compile source code, kemudian build aplikasi. Namun, seringkali hal-hal yang diperlukan untuk build aplikasi bukanlah hal yang diperlukan untuk menjalankan aplikasi yang kita kembangkan.