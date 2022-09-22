# Laporan Resmi Praktikum Jaringan Komputer Modul 1

## Anggota Kelompok
- 5025201248 - Fajar Zuhri Hadiyanto
- 5025201047 - Sidrotul Munawaroh

## Penjelasan Pengerjaan
### Nomor 1
Pertama, kita melakukan ping pada server monta untuk mendapatkan ip addressnya
![image](https://user-images.githubusercontent.com/94377420/191794346-ca32870b-97f1-4d24-a382-59f0916a1dea.png)
![image](https://user-images.githubusercontent.com/94377420/191794160-2bceb7bc-0db2-4cbb-91fa-62a6fd3d229e.png)
Maka didapatkan ip-nya yaitu 103.94.189.5. Ip address ini yang dijadikan sebagai filter
pada wireshark. Dengan filter protokol http dan ip src-nya, maka didapatkan server yang
digunakan, yaitu nginx

### Nomor 2
Gunakan filter request url untuk path “/detailTopik”. Didapatkan 1 buah paket yang berisi
info id detail topik, yaitu 194
![image](https://user-images.githubusercontent.com/94377420/191794734-80fb1731-371d-4131-8410-35bb8b9dd18f.png)
Nah, id ini yang dijadikan path menuju detail topiknya, maka didapatkan judulnya yaitu
“Evaluasi unjuk kerja User Space Filesystem (FUSE)”
![image](https://user-images.githubusercontent.com/94377420/191794840-cc834221-5d39-44fe-ac84-8723bbed3c4c.png)

### Nomor 3
Gunakan filter tcp.dstport pada display filter dengan value 80
![image](https://user-images.githubusercontent.com/94377420/191795357-b32f320f-127f-4d26-a555-29ea2f46a03b.png)

### Nomor 4
Gunakan tcp.src port untuk memfilter port asal dengan value 21
![image](https://user-images.githubusercontent.com/94377420/191795771-cf6b69e1-20b6-4785-b65e-9b5c38d08fde.png)

### Nomor 5
Sama halnya dengan nomor 4, namun ganti valuenya dengan 443
![image](https://user-images.githubusercontent.com/94377420/191796003-197a1ff2-dfd1-42c5-9d07-af4f4156df29.png)

### Nomor 6
Gunakan filter http.host dengan value yaitu match dengan lipi.go.id
![image](https://user-images.githubusercontent.com/94377420/191796143-c2aa8432-33db-406e-a9dc-e5a5acb9e03c.png)

### Nomor 7
Pada soal nomor 7, kita diminta untuk melakukan filter agar paket yang dicapture hanya yang berasal dari ip laptop kita. Pertama, kita cari tahu terlabih dahulu ip laptop kita pada adapter yang terhubung ke internet, dalam kasus ini, pada laptop saya menggunakan adapter wifi.

![ipconfig](https://user-images.githubusercontent.com/52820619/191510082-5ff4ff78-af4c-4160-9bb9-7dfe4267e4f9.png)

Dari gambar di atas, didapatkan ip-nya yaitu `192.168.1.22`. Maka gunakan capture filter `src host 192.168.1.22`. Maka didapatkan hasil berikut.

![filter dari ip kita](https://user-images.githubusercontent.com/52820619/191510100-f59b2bc2-9447-4f82-81cc-5f993b41bf64.png)

### Nomor 8
Pada soal nomor 8, kita diminta untuk menyadap percakapan antara dua mahasiswa dari package capture yang diberikan. Dari keterangan diberitahu bahwa percakapan dilakukan menggunakan protokol yang memiliki keandalan yang tinggi. Protokol yang dimaksud yaitu TCP, dan jika dilihat, terdapat 2 buah ip yang sering melakukan komunikasi, yaitu `127.0.0.1` dan `127.0.1.1`. Maka, tambah display filternya dengan asal kedua ip tersebut. Maka display filternya menjadi `tcp and (ip.src==127.0.0.1 or ip.src==127.0.1.1)`, maka didapatkan hasil sebagai berikut.

![image](https://user-images.githubusercontent.com/52820619/191513698-187b2b10-214c-4c4a-a801-465dc7f89811.png)

Setelah itu, kita bisa melakukan Follow tcp stream yang merupakan fitur pada wireshark, dan setelah itu, didapatkanlah percakapan antara kedua mahasiswa tersebut, yaitu sebagai berikut.

![percakapan](https://user-images.githubusercontent.com/52820619/191510117-74b07ec4-9dbb-4e4b-bdf5-4c424487b40e.png)

### Nomor 9
Pada soal nomor 9, kita diminta untuk mencari sebuah file yang dilaporkan terdapat pada sebuah transaksi oleh kedua mahasiswa tersebut. Kita diminta untuk menyimpan nama file tersebut menjadi `[nama kelompok].des3`, yaitu `E02.des3`. Kita juga diminta untuk melakukan dekripsi pada file tersebut menjadi `flag.txt`.

Untuk transaksinya sendiri, berdasarkan clue pada percakapan mereka, transaksi pertukaran file dilakukan pada port 9002. Sehingga kita perlu menggunakan filter tambahan berupa `tcp.port == 9002`, sehingga display filternya menjadim `tcp.port==9002 and (ip.src==127.0.0.1 or ip.src==127.0.1.1)`, maka didapatkan hasil sebagai berikut.

![image](https://user-images.githubusercontent.com/52820619/191516281-fc777ab9-571a-4021-81b9-2e70b84e48ac.png)

Lalu, kita lakukan Follow TCP stream, dan untuk pilihan show data as, kita pilih raw, untuk mendapatkan data mentah, maka didapatkan hasil sebagai berikut. data ini yang akan disimpan sebagai `E02.des3`

![image](https://user-images.githubusercontent.com/52820619/191510148-c3ef7bbb-358d-4476-b595-3f6c82150f2c.png)

File ini yang akan kita dekripsi menggunakan openssl dengan perintah `openssl des3 -d -in E02.des3 -out flag.txt`. Setelah itu, masukkan password yang diminta. Berdasarkan clue pada percakapan kedua mahasiswa tersebut (anime kembar lima), jawabannya yaitu **nakano**. Setelah itu, buka file `flag.txt`, maka hasilnya akan menjadi seperti berikut.

![image](https://user-images.githubusercontent.com/52820619/191510159-35407bf9-4ef4-4088-802e-841019fa9ca7.png)

### Nomor 10

Pada soal nomor 10, kita diminta untuk mencari tahu password rahasia (flag) nya. Sesuai dengan hasil pengerjaan nomor 9, flagnya merupakan isi dari `flag.txt`, yaitu `JaRkOm2022{8uK4N_CtF_k0k_h3h3h3}`

## Kendala Pengerjaan

Pada saat proses pengerjaan, terdapat beberapa kendala yaitu
- untuk nomor 8, sebelumnya kami belum mengetahui fitur 'Follow TCP stream' pada wireshark, sehingga kami harus membaca satu persatu isi dari pesan pada setiap paket
- untuk nomor 9 dan 10, sebelumnya kami belum mengetahui maksud dari soal dan ekspektasi output dari soal tersebut. Kami juga kurang memahami secara teknis cara mengerjakannya.
