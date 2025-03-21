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