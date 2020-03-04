![eksis](https://github.com/alimuamar11/workshopCloud/blob/master/Docker%20Commands/raung.png)
# Cubectl

```docker pull nginx```
```docker tag nginx alimuamar11/nginx:1.13```

# Mendownload image dari docker hub
1. Liat langsung di dockerhub apa yg mau di pull, misal mongo.

`#docker pull mongo` maka tag otomatis lates jika ingin versi berbeda maka :

`#docker pull mongo:4.1`

`#docker images` 

2. Membuat container dari image mongo yg udah di pull td

`#docker container create mongo:4.1` Disini nama container random, nanti susah ngafalin.

`#docker container create --name mongoserver1 mongo:4.1` (mongoserver1 bersifat unik maka tidak boleh sama jika mau buat 2 container dengan image sama.)

`#docker container ls` akan menampilkan container yg running "only running container"

`#docker container ls --all` semua container

3. Menjalankan container

`#docker container start mongoserver1` atau stop "remember" kalo ingin menghapus container harus di stop dulu container yg running.

4. Kq gk iso diakses soko jobo

`#docker container create --name mongoserver1 -p 8080:27017 mongo:4.1` dari luar container dpt diakses melalui port 8080 maka diforward requestnya ke container yg port nya 27017
port ini adalah milik internal container (mongo) misal akan dibuat 2 container dr image yang sama, maka :

`#docker container create --name mongoserver2 -p 8181:27017 mongo:4.1` "remember" nama unik dan port jangan sama(database), nanti pusing.

5. Hapus image

`#docker container stop mongoserver1 mongoserver2` di stop dulu containernya

`#docker container rm mongoserver1 mongoserver2` dihapus dulu containernya

`#docker image rm mongo:4.1`

# Membuat image dengan Dockerfile
1. Buat dulu aplikasinya dengan nama main.go 
2. Buat Dockerfile dengan ketentuan 

`FROM golang:1.11.4`

Tidak membuild image dari awal, maka digunakan `from` untuk mengambil images yang sudah ada.
golang adalah nama images yang telah tersedia, dengan tag nya adalah berupa versi dari images golang. yang bisa dilihat di website docker.

`COPY main.go /app/main.go`

kemudian mengcopy semua file `main.go` yang ada di local ke dalam image yang akan disimpan ke folder `app` dengan nama `main.go`

`CMD ["go","run","/app/main.go"]`

digunakan untuk me-runing file. diambil dari perintah running go yaitu `#go run main.go` tetapi ditambah perintah `CMD = command`

3. Build image dengan dr Dockerfile

`#docker build --tag app-golang:1.0 .` Membuild image menggunakan perintah `--tag` dengan nama image `app-golang` dan tag=`1.0`

4. Membuat container pada image yang barusan di build

`#docker container create --name app1 -p 8080:8080 app-golang:1.0`

Membuat container dengan nama app1 kemudian membuka port `-p` aplikasi biasanya default di 8080 kemudian di expose ke luar dengan port 8080 atau bisa 80 dalam image `app-golang:1.0` 

`#docker container ls --all` dilihat containernya

`#docker container start app1` dijalankan containernya

# Mengupload image
1. Buat repo di dockerhub
2. Balik ke terminal buat image baru dari image yang udah ada, karna dri dockerhub ditambah directori nama username dockerhub

`#docker tag app-golang:1.0 alimuamar/app-golang:1.0`

`#docker login`

`#docker push alimuamar/app-golang:1.0` 

3. Liat di repo udah ada belom.

# Melihat container docker

`#docker container inspect namacontainer`
`#docker container logs namacontainer`

# Masuk container

`#docker exec -t -i redis1 /bin/bash` misal masuk container redis (bisa lihat dockerdoc coy)
`#type redis-cli` memastikan
`#redis-cli` masuk cli punya redis, kalo mau keluar ya `#exit`

> Matursuwun
