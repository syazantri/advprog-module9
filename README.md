Reflection Module 9

> 1. What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?

- Metode unary RPC hanya melibatkan satu permintaan dan satu respons antara client dan server, berguna untuk operasi sederhana atau transaksional yang membutuhkan satu pertukaran data saja. 
- Server streaming RPC memungkinkan client mengirim satu permintaan dan menerima respons dalam bentuk aliran data. Ini sangat berguna ketika data perlu dikirimkan secara bertahap atau ketika ukuran data yang dikirimkan dari server ke client besar. 
- Bi-directional streaming RPC memungkinkan client dan server untuk saling mengirimkan aliran data secara simultan. Metode ini ideal untuk aplikasi yang membutuhkan komunikasi real-time dua arah, seperti chat atau pembaruan status langsung, di mana interaksi antara client dan server terjadi secara langsung.

> 2. What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?
<br>


Saat mengimplementasikan layanan gRPC di Rust, perlu memeriksa identitas pengguna atau layanan, dapat dilakukan melalui token seperti JWT atau dengan integrasi sistem OAuth2. Pengelolaan otorisasi diperlukan untuk mengendalikan akses ke sumber daya berdasarkan peran atau aturan yang ditetapkan, bisa diatur menggunakan middleware. Selain itu, untuk mengamankan komunikasi antara klien dan server, disarankan menggunakan enkripsi data, seperti melalui TLS, untuk mencegah penyadapan data dan menjaga kerahasiaan informasi yang ditransmisikan.

> 3. What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?


Saat mengimplementasikan streaming dua arah dengan gRPC di Rust, terutama untuk aplikasi chat, beberapa tantangan termasuk pengelolaan koneksi dan sinkronisasi pesan. Mengelola banyak koneksi secara bersamaan dan menjaga agar koneksi tetap aktif tanpa memberatkan server bisa rumit. Sistem juga perlu efisien dalam menangani aliran data masuk dan keluar untuk menghindari kelebihan beban (back pressure). Selain itu, penting untuk memastikan pesan dikirim dan diterima dalam urutan yang tepat serta disinkronkan antar pengguna.

> 4. What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services? 

Keuntungan:
- Memungkinkan pengelolaan secara asynchronou dan juuga terintegrasi dengan baik dengan tokio

Kekurangan:
- Dalam menghandle errornya lebih kompleks dan lebih tinggi kemungkinan overhead performa.

> 5. In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time? 

Untuk meningkatkan penggunaan ulang dan modularitas kode gRPC dalam Rust, beberapa teknik yang bisa diterapkan adalah:

- Menggunakan traits dan generics untuk komponen yang fleksibel dan konfigurasi ulang, memfasilitasi integrasi dan ekstensi fungsionalitas.
- Membagi kode menjadi modul atau crate berdasarkan fungsionalitas untuk pengelolaan dan penggunaan ulang kode yang lebih mudah.
- Mengadopsi library eksternal untuk tugas-tugas umum seperti serialisasi dan logging untuk meningkatkan konsistensi dan mengurangi duplikasi kode.

Dengan pendekatan ini, kode gRPC Rust akan lebih modular, mudah dipelihara, dan dapat diperluas dengan efisien.

> 6. In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?

Dapat ditingkatkan dengan validasi PaymentRequest untuk keamanan dan kelengkapan data. Server streaming lebih baik daripada unary untuk mentransfer data dalam jumlah besar.

Untuk menangani logika pembayaran yang lebih kompleks dalam implementasi MyPaymentService, langkah tambahan mungkin meliputi: pengelolaan transaksi yang lebih canggih, pemantauan status pembayaran real-time, dan penanganan transaksi gagal dengan lebih baik.

> 7. What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?

Adopsi gRPC memungkinkan interaksi yang lebih efisien antarmodul karena mengotomatisasi pemanggilan metode antarsistem melalui definisi di file proto. Ini menghilangkan kebutuhan untuk konfigurasi HTTP method secara manual. gRPC, yang berbasis pada HTTP/2, mendukung komunikasi yang cepat dan efisien antara layanan, dengan kemampuan streaming yang baik dan overhead rendah, jadi interaksinya bakal lebih efektif.

> 8. What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?
     
HTTP/2 kelebihannya adalah punya konsep multiplexing yaitu bisa handle banyak request response dalam single connection, juga ada prioritas sehingga server bisa kirim sebelum diiminta client biar sampainya tepat waktu.

Kekurangannya adalah lebiih kompleks dan baru, jadi sulit didukung secara universal.

> 9. How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?

Request-response modelnya rest api itu lebih ga efisien karena biasanya 1 request untuuk 1 reponse, tapi kalau gRPC dengan stream dua arah itu jadi bisa bareng request response jadi lebih efisien.

> 10. What are the implications of the schema-based approach of gRPC, using Protocol Buffers, compared to the more flexible, schema-less nature of JSON in REST API payloads?

gRPC dengan Protocol Buffers memakai skema yang kaku, beda dari JSON yang bebas. Protocol Buffers bikin kirim data jadi lebih efisien karena strukturnya selalu konsisten dan bisa dicek. Ini bagus buat sistem besar yang butuh jelasin data. JSON lebih fleksibel tapi bisa bikin sulit ngecek data karena strukturnya bisa berubah-ubah tanpa kabar.







