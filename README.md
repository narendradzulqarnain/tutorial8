# tutorial8

a. What is amqp?  
AMQP (Advanced Message Queuing Protocol) adalah *open standard protocol* yang membuat aplikasi-aplikasi atau komponen-komponen bisa saling berkomunikasi melalui pesan.

b. what it means? guest:guest@localhost:5672 , what is the first quest, and what is
the second guest, and what is localhost:5672 is for?  
`guest:guest@localhost:5672` adalah URI *connection* untuk AMQP. 'guest' yang pertama adalah *username* yang digunakan untuk autentikasi dengan AMQP broker dan 'guest' yang kedua adalah passwordnya.

a. How many data your publlsher program will send to the message broker in one run?  
Publisher akan mengirimkan 5 data ke *message broker*. Setiap pemanggilan method `publish_event` mengirimkan satu *instance* dari `UserCreatedEventMessage` ke *broker*.

b. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber
program, what does it mean?  
Kedua program akan terhubung ke AMQP yang sama.

![alt text](image.png)

![alt text](image-1.png)
Terminal di kanan adalah *publisher* dan di kiri adalah *subscriber*. Ketika dijalankan `cargo run` pada *publisher*, program mengirimkan 5 event ke *message broker* lalu diproses oleh *subscriber*.

![alt text](image-2.png)
Ketika dijalankan `cargo run` pada publisher, publisher akan mengirimkan message. Chart kedua menunjukkan *message rate* sehingga ketika publisher mengirimkan message akan terbaca dan ditampilkan pada chart.

![alt text](image-3.png)
Karena subscriber memproses dengan lambat, event-event yang dikirimkan ditaruh diantrian terlebih dahulu. Saya menjalankan `cargo run` sebanyak 5 kali, sehingga ada 25 event yang dikirimkan. Chart Queued message menunjukkan angka sekitar 16, artinya sebanyak 16 event ditaruh pada antrian dan menunggu untuk diproses oleh subscriber.

![alt text](image-5.png)
Dengan menjalankan subscriber pada 3 console berbeda, ketika publisher mengirimkan event, pemrosesan event oleh subscriber dibagi pada ketiga console.
![alt text](image-4.png)
Spike pada chart queued messages juga berkurang lebih cepat dibandingkan sebelumnya. Hal ini disebabkan oleh ketiga program subscriber yang dapat memproses event secara paralel. Oleh karena itu, message yang ada pada antrian juga dapat diproses lebih cepat.  

Salah satu hal yang dapat ditingkatkan pada program adalah *error handling*. Contohnya, pada `main.rs` subscriber dapat ditambahkan *error handling* untuk `unwrap()` yang dapat menyebabkan program *panic* jika terjadi error.