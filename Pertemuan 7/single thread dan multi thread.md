# LAPORAN LATIHAN SISTEM OPERASI

<img src="pngegg.png" width="240">


## DOSEN PENGAMPU
Dr. Ferry Astika Saputra, ST, M.Sc

## NAMA PEMBUAT
MUCHAMMAD HAWWIN ROMADHON

KELAS : IT A

NRP : 3124521003

POLITEKNIK ELEKTRONIKA NEGERI SURABAYA PSDKU LAMONGAN

---

### PENJELASAN SINGLE THREAD DAN MULTI THREAD

• Single Thread

<img src="single thread.png" width="600">

Single-threading adalah pendekatan di mana sebuah proses hanya menjalankan satu thread eksekusi. Seperti terlihat pada gambar, proses single-threaded terdiri dari code, data, dan file yang digunakan bersama dengan satu set register, program counter (PC), dan stack milik thread tersebut. Karena hanya ada satu thread, eksekusi program berjalan secara sekuensial—artinya setiap tugas harus diselesaikan sebelum berpindah ke tugas berikutnya. Pendekatan ini lebih sederhana dan mudah dikelola karena tidak memerlukan sinkronisasi antar thread, tetapi kurang efisien untuk tugas yang membutuhkan paralelisme atau responsivitas tinggi, seperti aplikasi modern yang perlu menangani banyak operasi secara bersamaan

Kelemahan utama single-threading terlihat ketika proses menghadapi operasi blocking, misalnya menunggu input pengguna atau pembacaan file. Selama tugas tersebut belum selesai, seluruh aplikasi akan terhenti (freeze) karena tidak ada thread lain yang bisa mengambil alih. Contoh klasiknya adalah program CLI (Command Line Interface) yang menjalankan perintah satu per satu. Meskipun terbatas, single-threading masih berguna untuk aplikasi sederhana atau sistem dengan sumber daya terbatas, seperti perangkat embedded, di mana kompleksitas multi-threading tidak diperlukan

---

• Multi Thread

<img src="multi thread.png" width="600">

Multi-threading adalah teknik pemrograman yang memungkinkan sebuah proses menjalankan beberapa thread secara bersamaan dalam satu lingkungan eksekusi. Setiap thread memiliki komponen privat seperti register, stack, dan program counter (PC) yang memungkinkannya berjalan secara independen. Namun, semua thread dalam proses yang sama berbagi sumber daya seperti kode program, data, dan file, sehingga komunikasi antar thread lebih efisien dibandingkan antar proses. Teknik ini meningkatkan kinerja aplikasi dengan memanfaatkan CPU multi-core dan menjaga responsivitas sistem, misalnya pada aplikasi GUI yang tetap lancar meskipun sedang melakukan komputasi berat

Keunggulan multi-threading terletak pada kemampuannya mengoptimalkan penggunaan sumber daya sistem. Dibandingkan membuat banyak proses, thread lebih ringan karena tidak memerlukan alokasi memori terpisah. Contohnya, web browser modern menggunakan multi-threading untuk menangani tab secara paralel—satu thread mengelola antarmuka pengguna, sementara thread lain memuat konten atau menjalankan script. Tantangannya adalah mengelola sinkronisasi antar thread untuk menghindari race condition, tetapi dengan implementasi yang tepat, multi-threading bisa menjadi solusi efisien untuk aplikasi yang membutuhkan konkurensi tinggi

---

SELESAI
