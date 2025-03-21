# Tutorial Module 6

```
Nama    : Rakha Abid Bangsawan
NPM     : 2206081585
Kelas   : B
```

1. Commit 1 - `handle_connection` Function

   ```
   fn handle_connection(mut stream: TcpStream) {
       let buf_reader = BufReader::new(&mut stream);
       let http_request: Vec<_> = buf_reader
           .lines()
           .map(|result| result.unwrap())
           .take_while(|line| !line.is_empty())
           .collect();

       println!("Request: {:#?}", http_request);
   }
   ```

   Berdasarkan informasi dari [dokumentasi Rust](https://doc.rust-lang.org/book/ch20-01-single-threaded.html), fungsi `handle_connection` berfungsi untuk menangani koneksi yang masuk ke server. Fungsi ini pertama-tama membuat instance `BufReader`, yang membungkus referensi *mutable* ke `stream`.

    Kemudian, variabel `http_request` digunakan untuk mengumpulkan baris-baris permintaan HTTP yang dikirimkan oleh browser ke server. Metode `lines()` dari `BufReader` menghasilkan iterator yang mengembalikan `Result<String, std::io::Error>`. Selanjutnya, baris-baris yang diterima dikumpulkan dalam sebuah vektor hingga ditemukan baris kosong, yang menandai akhir dari permintaan HTTP (karena browser mengakhiri permintaan dengan dua karakter *new line* berturut-turut).

    Dengan cara ini, fungsi `handle_connection` bertanggung jawab membaca dan memproses permintaan HTTP dari *stream* yang diterima oleh server.


2. Commit 2 - Returning HTML
    ![alt text](image.png)

    Beberapa tambahan kode terlihat setelah variabel `http_request`. Terdapat variabel `status_line` untuk status dari *request*. Lalu, program membaca file `hello.html` menggunakan `fs::read_to_string` dan menyimpannya ke variable `contents`. Ada juga variable `length` yang merepresentasikan panjang dari variabel `contents`. Selanjutnya, respon akan disimpan ke variabel `response`. `format!` akan digunakan untuk konten file sebagai *response body*. 

    `http_request` akan di-*ignore* sehingga semua *request* akan diterima dan akan mengembalikan *file* `hello.html`, artinya *request* `127.0.0.1:7878/sesuatu` juga akan mengembalikan respon yang sama.