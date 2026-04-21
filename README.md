# Tutorial 6 - Web Server

**Nama:** Ryan Gibran Purwacakra Sihaloho
**NPM:** 2406419833

---

## Commit 1 Reflection notes

Pada *commit* ini, saya menambahkan fungsi `handle_connection` untuk membaca dan memproses *request* TCP yang masuk dari *browser*. 
Fungsi ini menggunakan `BufReader` yang membungkus `TcpStream` agar pembacaan aliran data dari klien menjadi lebih efisien. 
Data *request* HTTP tersebut kemudian dibaca baris per baris menggunakan metode `.lines()`. 
Program akan terus membaca teks tersebut dan mengumpulkannya ke dalam sebuah struktur data *vector* bernama `http_request` melalui metode `.collect()`. 
Proses pembacaan ini diinstruksikan untuk berhenti secara otomatis ketika menemukan baris kosong, yang ditangani oleh metode `.take_while(|line| !line.is_empty())`. 
Terakhir, program mencetak keseluruhan isi *request* tersebut ke terminal sehingga saya dapat menganalisis detail informasi yang dikirimkan oleh klien, seperti tipe metode HTTP (GET), *host* tujuan, dan data *user-agent*.

## Commit 2 Reflection notes

![Commit 2 screen capture](assets/images/commit2.png)

Pada tahapan ini, saya memodifikasi fungsi `handle_connection` agar server tidak hanya membaca *request*, tetapi juga memberikan *response* yang valid berupa halaman HTML. 
Saya menambahkan modul `fs` (File System) dari standard library Rust untuk membaca isi file `hello.html` ke dalam bentuk *string*. 
Setelah file terbaca, saya menyusun HTTP *response* yang terdiri dari *status line* (`HTTP/1.1 200 OK`), *header* `Content-Length` (menandakan ukuran konten), dan diakhiri dengan isi (body) HTML tersebut yang dipisahkan oleh karakter baris baru ganda (`\r\n\r\n`). 
Terakhir, `stream.write_all()` digunakan untuk mengirimkan sekumpulan *byte* dari variabel *response* kembali ke klien melalui koneksi TCP. Perubahan ini membuat web server kini dapat menampilkan antarmuka web sederhana secara langsung di browser.