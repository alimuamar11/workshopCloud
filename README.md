# workshopCloud/ cubectl

```docker pull nginx```
```docker tag nginx alimuamar11/nginx:1.13```

# Membuat images dengan Dockerfile
1. Aplikasi golang yaitu main.go
2. File Dockerfile
`FROM golang:1.11.4`
Tidak membuild image dari awal, maka digunakan `from` untuk mengambil images yang sudah ada.
golang adalah nama images yang telah tersedia, dengan tag nya adalah berupa versi dari images golang. yang bisa dilihat di website docker.

`COPY main.go /app/main.go`
kemudian mengcopy semua file `main.go` ke dalam images yang akan disimpan ke folder `app` dengan nama `main.go`

`CMD ["go","run","/app/main.go"]`
digunakan untuk me-runing file. diambil dari perintah running go yaitu `#go run main.go` tetapi ditambah perintah `CMD = command`
3. docker build --tag app-golang:1.0 .
Membuild images menggunakan perintah `--tag` dengan nama images `app-golang` dan tag=`1.0`
4. docker images
5. docker container create --name app1 -p 8080:8080 app-golang:1.0
Membuat container dari `app-golang` dengan nama app1 kemudian membuka port `-p`
aplikasi biasanya defauld di 8080 kemudian di expose ke luar dengan port 8080 atau bisa 80 kemudian nama images yaitu `app-golang:10` 
6. docker container ls -all
7. docker container start app1