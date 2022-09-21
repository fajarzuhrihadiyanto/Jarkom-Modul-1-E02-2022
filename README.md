# Laporan Resmi Praktikum Jaringan Komputer Modul 1

## Anggota Kelompok
- 5025201248 - Fajar Zuhri Hadiyanto
- 5025201047 - Sidrotul Munawaroh

## Penjelasan Pengerjaan
### Nomor 1

### Nomor 2

### Nomor 3

### Nomor 4

### Nomor 5

### Nomor 6

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

### Nomor 10
