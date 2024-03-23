Nama: Lucinda Laurent<br>
Kelas: Adpro B<br>
NPM: 2206024745<br>

## Refleksi Tutorial 6
#### Commit 1 Reflection notes: what is inside the handle_connection method?
`handle_connection` method digunakan untuk membaca data dari TCP (Transmission Control Protocol) stream dan mencetaknya sehingga kita bisa melihat data yang dikirim dari browser. Pada `handle_connection` method, kita membuat instance BufReader yang membungkus mutable reference ke stream. Kemudian kita membuat variabel bernama `http_request` yang akan menyimpan semua baris request yang dikirim dari browser ke server kita ke dalam sebuah vector. Method `lines` akan mengembalikan iterator berupa `Result<String, std::io::Error>` dengan membagi data dari stream sesuai baris-barisnya(ditandai dengan adanya newline byte). Kemudian kita memetakan dan `unwrap` setiap `Result` untuk mendapatkan String tiap barisnya. `take_while` digunakan untuk terus membaca semua baris yang ada sampai program menemukan baris kosong, yang menandakan akhir dari sebuah HTTP request. Setelah semua baris tersimpan di vector, program akan mencetak baris-baris tersebut menggunakan debug formatting yang sudah diatur.
#### Commit 2 Reflection notes: the new handle_connection
![Commit 2 screen capture](assets/images/commit2.png)
Method handle_connection yang baru memungkinkan kita untuk menampilkan pesan tertentu pada halaman html, tidak hanya mencetak di console seperti sebelumnya. <br>
Response terhadap request dari client mengikuti format
```
HTTP-Version Status-Code Reason-Phrase CRLF
headers CRLF
message-body
```
Mengikuti format tersebut, pertama-tama kita buat variabel `status_line` untuk menyimpan HTTP version 1.1, dengan kode status 200, dan reason-phrase "OK". Kita menggunakan `fs::read_to_string` untuk membaca isi file `hello.html` sebagai String. String hasil pembacaan tersebut akan digunakan sebagai body dari response menggunakan `format!`. Untuk memastikan HTTP response-nya valid, kita juga menambahkan header berupa `Content-Length` yang diatur menyesuaikan panjang dari response body alias panjang String hasil pembacaan `hello.html`. HTTP-Version Status-Code Reason-Phrase, header, dan message-body tersebut disatukan menggunakan `format!` yang disimpan sebagai variabel `response`. Terakhir, String `response` tersebut diconvert ke byte dan dikirim ke server. 
