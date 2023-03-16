# Learn Basic Docker

Catatan belajar Docker. referensi dari [Programmer Zaman Now - TUTORIAL DOCKER DASAR](https://www.youtube.com/watch?v=3_yxVjV88Zk)

## Check Version

`docker version` or `docker --version`

## Docker Images
Docker Image mirip seperti installer aplikasi, dimana di dalam Docker Image terdapat aplikasi dan dependency. 

Sebelum kita bisa menjalankan aplikasi di Docker, kita perlu memastikan memiliki Docker Image aplikasi tersebut.

#### View Docker Images
`docker images` or `docker image ls`

#### Download/Pull Docker Image
`docker pull <image_name>:<tag>`

Kita bisa mencari Docker Image yang ingin kita download di [https://hub.docker.com/](https://hub.docker.com/)

#### Delete Docker Image
`docker rmi <image_name>:<tag>` or `docker image rm <image_name>:<tag>`

## Docker Container
Jika Docker Image seperti installer aplikasi, maka Docker Container mirip seperti aplikasi hasil installernya. 

Satu Docker Image bisa digunakan untuk membuat beberapa Docker Container, asalkan nama Docker Container nya berbeda.

Jika kita sudah membuat Docker Container, maka Docker Image yang digunakan tidak bisa dihapus, hal ini dikarenakan sebenarnya Docker Container tidak meng-copy isi Docker Image, tapi hanya menggunakannya isinya saja

#### Container Status
Saat kita membuat container, secara default container tersebut tidak akan berjalan.

Mirip seperti ketika kita menginstall aplikasi, jika tidak kita jalankan, maka aplikasi tersebut tidak akan berjalan, begitu juga container.

Oleh karena itu, setelah membuat container, kita perlu menjalankannya jika memang ingin menjalankan container nya.

#### View Docker Container
`docker ps` or `docker container ls` untuk melihat container yang running
`docker ps -a` `docker container ls -a` untuk melihat semua container, baik yang running maupun tidak

#### Create Docker Container
`docker container create --name <container_name> <image_name>:<tag>`

#### Running Docker Container
`docker container start <container_name>`

#### Create and Running Docker Container
`docker run -d --name <container_name> <image_name>:<tag>`

option `-d` merupakan singkatan dari detach, biasanya digunakan untuk aplikasi yang memerlukan untuk _running in background_.

#### Delete Docker Container
`docker container rm <nama_container>` or `docker rm <nama_container>`

command lainnya yang sama:

`docker rm -f <nama_container>`

digunakan untuk menghapus container yang masih running, option `-f` yaitu _force_.

## Container Logs
Biasanya dilakukan untuk melihat detail kejadian apa yang terjadi di aplikasi, sehingga akan memudahkan kita ketika mendapat masalah.

command:

`docker logs <nama_container>`

atau jika ingin secara realtime bisa menggunakan perintah:

`docker logs -f <nama_container>`

## Container Exec
Untuk masuk ke dalam container, kita bisa mencoba mengeksekusi program bash script yang terdapat di dalam container dengan bantuan Container Exec, dengan perintah:

`docker exec -it <nama_container> /bin/sh`

`-i` adalah argument interaktif, menjaga input tetap aktif

`-t` adalah argument untuk alokasi pseudo-TTY (terminal akses)

Dan `/bin/sh` contoh kode program yang terdapat di dalam container, yang berarti ini untuk menjalankan shell dengan sh.

## Container Port
Saat menjalankan container, container tersebut terisolasi di dalam Docker, artinya sistem Host (misal Laptop kita), tidak bisa mengakses aplikasi yang ada di dalam container secara langsung, salah satu caranya adalah harus menggunakan Container Exec untuk masuk ke dalam container nya.

Biasanya, sebuah aplikasi berjalan pada port tertentu, misal saat kita menjalankan aplikasi Nginx sebagai web server, dia berjalan pada port 80, kita bisa melihat port apa yang digunakan ketika melihat semua daftar container.

Docker memiliki kemampuan untuk melakukan port forwarding, yaitu meneruskan sebuah port yang terdapat di sistem Host nya ke dalam Docker Container.

Cara ini cocok jika kita ingin mengekspos port yang terdapat di container ke luar melalui sistem Host nya.

#### Port Forwarding
Untuk melakukan port forwarding, kita bisa menggunakan perintah berikut ketika membuat container nya :
`docker container create --name <container_name> --publish <port_host>:<port_container> <image>:<tag>`

Jika kita ingin melakukan port forwarding lebih dari satu, kita bisa tambahkan dua kali parameter `--publish`

`--publish` juga bisa disingkat menggunakan `-p`

misal:
`docker container create --name <container_name> --p <port_host>:<port_container> --p <port_host>:<port_container> <image>:<tag>`

## Container Environment Variable
Saat membuat aplikasi, menggunakan Environment Variable adalah salah satu teknik agar konfigurasi aplikasi bisa diubah secara dinamis.

Dengan menggunakan environment variable, kita bisa mengubah-ubah konfigurasi aplikasi, tanpa harus mengubah kode aplikasinya lagi.

Docker Container memiliki parameter yang bisa kita gunakan untuk mengirim environment variable ke aplikasi yang terdapat di dalam container.

Untuk menambah environment variable, kita bisa menggunakan perintah --env atau -e, misal :
`docker container create --name <container_name> --env KEY="value" --env KEY2="value" <image>:<tag>`

atau contoh real kita akan running aplikasi MySQL Database dengan env database dan password:
`docker run --name mysqldb -e MYSQL_ROOT_PASSWORD=my-secret-pw -e MYSQL_DATABASE=mydb -d mysql:8.0.29`

## Docker Volume
Sebelumnya di Docker ada fitur Bind Mounts sejak Docker versi awal, di versi terbaru direkomendasikan menggunakan Docker Volume.

Volume sendiri bisa dianggap storage yang digunakan untuk menyimpan data, bedanya dengan Bind Mounts, pada bind mounts, data disimpan pada sistem host, sedangkan pada volume, data di manage oleh Docker

#### View Volume
`docker volume ls`

#### Create Volume
`docker volume create <volume_name>`

#### Menghapus Volume
`docker volume rm <volume_name>`

## Container Volume
Volume yang sudah kita buat, bisa kita gunakan di container.

Keuntungan menggunakan volume adalah, jika container kita hapus, data akan tetap aman di volume.

Cara menggunakan volume di container menggunakan type atau parameter volume dan source nama volume.

contoh:
`docker create volume mysqldata`
`docker container create --name mysqldb-1 -e MYSQL_ROOT_PASSWORD=my-secret-pw -e MYSQL_DATABASE=mydb -v mysqldata:/var/lib/mysql -p 3306:3306 mysql:8.0.29`

## Docker Network
Saat kita membuat container di docker, secara default container akan saling terisolasi satu sama lain, jadi jika kita mencoba memanggil antar container, bisa dipastikan bahwa kita tidak akan bisa melakukannya.

Docker memiliki fitur Network yang bisa digunakan untuk membuat jaringan di dalam Docker.

Dengan menggunakan Network, kita bisa mengkoneksikan container dengan container lain dalam satu Network yang sama.

Jika beberapa container terdapat pada satu Network yang sama, maka secara otomatis container tersebut bisa saling berkomunikasi.


#### Network Driver
Saat kita membuat Network di Docker, kita perlu menentukan driver yang ingin kita gunakan, ada banyak driver yang bisa kita gunakan, tapi kadang ada syarat sebuah driver network bisa kita gunakan.

* <b>bridge</b>, yaitu driver yang digunakan untuk membuat network secara virtual yang memungkinkan container yang terkoneksi di bridge network yang sama saling berkomunikasi.

* <b>host</b>, yaitu driver yang digunakan untuk membuat network yang sama dengan sistem host. host hanya jalan di Docker Linux, tidak bisa digunakan di Mac atau Windows.

* <b>none</b>, yaitu driver untuk membuat network yang tidak bisa berkomunikasi 

#### View Docker Network
`docker network ls`

#### Create Docker Network
`docker network create <nama_network>`

#### Delete Docker Network
`docker network rm <nama_network>`

## Container Network
Setelah kita membuat Network, kita bisa menambahkan container ke network.

Container yang terdapat di dalam network yang sama bisa saling berkomunikasi (tergantung jenis driver network nya).

Container bisa mengakses container lain dengan menyebutkan hostname dari container nya, yaitu nama container nya.

Untuk menambahkan container ke network, kita bisa menambahkan perintah `--network` ketika membuat container, misal :
`docker container create --name <nama_container> --network <nama_network> <image>:<tag>`

#### Use Case Container Network
create network
`docker create network mongoapp`

running mongo container
`docker run -d --name mongodb --network mongoapp -e MONGO_INITDB_ROOT_USERNAME=piscki -e MONGO_INITDB_ROOT_PASSWORD=nopassword mongo`

running website container yang connect ke mongodb
`docker run -dp 8081:8081 -e ME_CONFIG_MONGODB_URL="mongodb://piscki:nopassword@mongodb:27017/" mongo-express`

#### Delete Container from Network
Jika diperlukan, kita juga bisa menghapus container dari network dengan perintah :
`docker network disconnect <nama_network> <nama_container>`

#### Add Container to Network
Jika containernya sudah terlanjur dibuat, kita juga bisa menambahkan container yang sudah dibuat ke network dengan perintah :
`docker network connect <nama_network> <nama_container>`

## Inspect
Setelah kita men-download image, atau membuat network, volume dan container. Kadang kita ingin melihat detail dari tiap hal tersebut

Misal kita ingin melihat detail dari image, perintah apa yang digunakan oleh image tersebut? Environment variable apa yang digunakan? Atau port apa yang digunakan?

Misal kita juga ingin melihat detail dari container, Volume apa yang digunakan? Environment variable apa yang digunakan? Port forwarding apa yang digunakan? dan lain-lain

Docker memiliki fitur bernama inspect, yang bisa digunakan di image, container, volume dan network

Dengan fitur ini, kita bisa melihat detail dari tiap hal yang ada di Docker

#### Using Inspect
* Untuk melihat detail dari image, gunakan : `docker image inspect <nama_image>`
* Untuk melihat detail dari container, gunakan : `docker container inspect <nama_container>`
* Untuk melihat detail dari volume, gunakan : `docker volume inspect <nama_volume>`
* Untuk melihat detail dari network, gunakan : `docker network inspect <nama_network>`

## Prune
Saat kita menggunakan Docker, kadang ada kalanya kita ingin membersihkan hal-hal yang sudah tidak digunakan lagi di Docker, misal container yang sudah di stop, image yang tidak digunakan oleh container, atau volume yang tidak digunakan oleh container

Fitur untuk membersihkan secara otomatis di Docker bernama prune

Hampir di semua perintah di Docker mendukung prune

#### Using Prune
* Untuk menghapus semua container yang sudah stop, gunakan : `docker container prune`
* Untuk menghapus semua image yang tidak digunakan container, gunakan : `docker image prune`
* Untuk menghapus semua network yang tidak digunakan container, gunakan : `docker network prune`
* Untuk menghapus semua volume yang tidak digunakan container, gunakan : `docker volume prune`
* Atau kita bisa menggunakan satu perintah untuk menghapus container, network dan image yang sudah tidak digunakan menggunakan perintah : `docker system prune`

### Finish Chapter

Silahkan lanjut ke Project Berikutnya: [Dockerized Local Environment Development](https://github.com/pisckipratama/docker-notes/tree/main/1-dockerized-local-env)