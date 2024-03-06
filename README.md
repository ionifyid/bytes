# Bytes-API

## Daftar isi

- [Tentang](#tentang)
- [Panduan Menjalankan](#panduan-menjalankan)
- [Struktur Project](#struktur-project)
- [Dokumentasi API](#dokumentasi-api)

## Tentang

Bytes API merupakan REST API untuk mendapatkan data course dan login user yang telah terdaftar disistem. Pada API ini juga untuk mendapatkan rekomendasi course dari API Machine-Learning.

## Panduan Menjalankan

Proses menjalankan API ini dapat dilakukan dengan 2 cara yaitu menjalankan file main secara langsung atau menggunakan docker. Berikut merupakan penjelasan cara menjalankan proyek ini:

### Langsung

Clone project ini ke directory GOPATH anda

#### Environment Variables

Untuk menjalankan proyek ini, Anda perlu menambahkan variabel berikut ke file .env Anda

`HOST`

`USER`

`PASSWORD`

`DBNAME`

`JWT_KEY`

Kemudian jalankan file main.go dengan command sebagai berikut:

```go
  go run main.go
```

### Docker

Clone project ini di directory manapun. Kemudian buat file Dockerfile dengan isi seperti berikut:

```Dockerfile
FROM golang:1.20-alpine

ENV DB_HOST=
ENV DB_USER=
ENV DB_PASS=
ENV DB_NAME=
ENV JWT_KEY=

ADD . /go/src/app
WORKDIR /go/src/app

COPY go.mod ./
COPY go.sum ./
RUN go mod download

COPY *.go ./

CMD go run main.go
```

NOTE: Jangan lupa sesuaikan isi variabel ENV-nya

```docker
docker build -t bytes-api .
```

```docker
docker container run --name bytes-api -d -p 8080:8080 bytes-api
```

## Struktur-project

Secara sederhana project ini dibuat dengan menggunakan struktur Clean Architecture yang dipopulerkan oleh Uncle Bob. Berikut merupakan struktur Clean Architecture versi Uncle Bob:

![Clean Architecture](https://user-images.githubusercontent.com/13291041/102681893-84326980-4208-11eb-8f84-2959e03b89d8.png)

Dengan detail direktori dan file yang menyusun project sebagai berikut:

```bash
├── main.go
├── controller
│   ├── course.go
│   ├── user_course.go
│   └── user.go
├── database
│   └── database.go
├── helper
│   └── helper.go
├── jwt
│   └── jwt.go
├── middleware
│   └── middleware.go
├── models
│   ├── course.go
│   ├── user_course.go
│   └── user.go
├── repository
│   ├── course.go
│   ├── user_course.go
│   └── user.go
├── routes
│   └── routes.go
├── service
│   ├── course.go
│   ├── user_course.go
│   └── user.go
├── src
│   └──  images
```

## Dokumentasi API

Berikut merupakan dokumentasi API yang telah dibuat:

| Method | Endpoint                   | Description               |
| ------ | -------------------------- | ------------------------- |
| POST   | /auth/register             | Register user             |
| POST   | /auth/login                | Login user                |
| Get    | /auth/user                 | Get user info             |
| POST   | /like/:courseid            | Like course               |
| DELETE | /like/:courseid            | Unlike course             |
| GET    | /course                    | Get recommendation course |
| GET    | /course/material/:courseid | Get material course       |
| GET    | /course/quiz/:courseid     | Get quiz course           |
| GET    | /course/summary/:courseid  | Get summary course        |
