## Panduan menjalankan “order-page”

**Teknologi :**

-	Docker
-	RabbitMQ (melalui container apabila menggunakan docker)
-	Golang (telah dijalankan pada golang versi 1.11 – 1.15)


**Menjalankan “user-credential” sebagai server :**

-	Buka terminal pada direktori “user-credential”
-	Lakukan export DATA_SOURCE dan ENV pada terminal
-	Jalankan “user credential” dengan menuliskan perintah : `go run main.go`


**Docker untuk menjalankan RabbitMQ :**

-	Jalankan container pada terminal dengan menuliskan perintah : `docker run -it --rm --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3-management` 
-	RabbitMQ dapat diakses melalui : http://localhost:15672/
-	Masukkan username dan password untuk login (default username : guest, default password : guest)
-	Setelah login, dapat terlihat setiap queue, pesan yang terdapat pada queue, dan status lainnya


**Menjalankan “order-page” :**

-	Pastikan server dan RabbitMQ sedang berjalan
-	Buka terminal pada direktori “order-page”
-	Lakukan export DATA_SOURCE, WORKER_URL, CRED_URL, GO_ENV, dan APIGATEWAY_URL pada terminal. 
-	Jalankan “order-page” dengan menuliskan perintah : `go run main.go` 

**Melakukan trigger terhadap “order-page” :**

-	Buka terminal pada direktori “trigger-order-page”
-	Jalankan trigger dengan menuliskan perintah :
`go run send_trigger_category.go`
- Apabila trigger berhasil dilakukan, maka akan tampil request body yang dikirimkan ke API Gateway dan responnya akan dikirimkan ke RabbitMQ dengan nama queue "polling-order-unit"
