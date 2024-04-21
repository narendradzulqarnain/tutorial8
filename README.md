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