Nama: Lucinda Laurent<br>
Kelas: Adpro B<br>
NPM: 2206024745<br>

## Refleksi Tutorial 6
#### Commit 1 Reflection notes: what is inside the handle_connection method?
`handle_connection` method digunakan untuk membaca data dari TCP (Transmission Control Protocol) stream dan mencetaknya sehingga kita bisa melihat data yang dikirim dari browser. Pada `handle_connection` method, kita membuat instance BufReader yang membungkus mutable reference ke stream. Kemudian kita membuat variabel bernama `http_request` yang akan menyimpan semua baris request yang dikirim dari browser ke server kita ke dalam sebuah vector. Method `lines` akan mengembalikan iterator berupa `Result<String, std::io::Error>` dengan membagi data dari stream sesuai baris-barisnya(ditandai dengan adanya newline byte). Kemudian kita memetakan dan `unwrap` setiap `Result` untuk mendapatkan String tiap barisnya. `take_while` digunakan untuk terus membaca semua baris yang ada sampai program menemukan baris kosong, yang menandakan akhir dari sebuah HTTP request. Setelah semua baris tersimpan di vector, program akan mencetak baris-baris tersebut menggunakan debug formatting yang sudah diatur.