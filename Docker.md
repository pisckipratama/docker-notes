# Learn Basic Docker

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
