# Learn Basic Docker

Catatan belajar Docker. referensi dari [Programmer Zaman Now - TUTORIAL DOCKER DASAR](https://www.youtube.com/watch?v=3_yxVjV88Zk)

### Check Version

`docker version` or `docker --version`

### Docker Images
Docker Image mirip seperti installer aplikasi, dimana di dalam Docker Image terdapat aplikasi dan dependency. 

Sebelum kita bisa menjalankan aplikasi di Docker, kita perlu memastikan memiliki Docker Image aplikasi tersebut.

#### View Docker Images
`docker images` or `docker image ls`

#### Download/Pull Docker Image
`docker pull <image_name>:<tag>`

Kita bisa mencari Docker Image yang ingin kita download di [https://hub.docker.com/](https://hub.docker.com/)

#### Delete Docker Image
`docker rmi <image_name>:<tag>` or `docker image rm <image_name>:<tag>`

### Docker Container
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