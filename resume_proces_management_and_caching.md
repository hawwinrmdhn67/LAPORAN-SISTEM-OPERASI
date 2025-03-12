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

1.35 Process Management

    Proses adalah program yang sedang dieksekusi, berbeda dengan program yang hanya merupakan entitas pasif

    Sumber daya yang dibutuhkan: CPU, memori, I/O, file, dan data inisialisasi

    Manajemen proses mencakup :

        1.Membuat dan menghapus proses

        2.Menangguhkan dan melanjutkan proses
    
        3.Menyediakan mekanisme sinkronisasi dan komunikasi antar-proses
    
        4.Menangani kondisi deadlock
        
 ---   

1.36 Process Management Activities
    
    Sistem operasi bertanggung jawab atas pengelolaan proses, termasuk: 
    
        1.Pembuatan dan penghapusan proses
        
        2.Penjadwalan CPU: Memilih proses yang akan dieksekusi
        
        3.Sinkronisasi proses: Menghindari konflik dalam penggunaan sumber daya bersama
        
        4.Komunikasi antar-proses: Berbagi data antar proses
        
        5.Penanganan deadlock: Mengelola kondisi di mana dua atau lebih proses saling menunggu sumber daya

---

1.37 Memory Management

    Agar program dapat dieksekusi, sebagian atau seluruh instruksi serta data harus ada di memori
    
    Manajemen memori mencakup: 
    
        1.Menjaga informasi tentang bagian memori yang digunakan
        
        2.Menentukan data dan proses mana yang dimuat ke dalam memori
        
        3.Mengalokasikan dan membebaskan memori sesuai kebutuhan
        
---

1.38 File-System Management

    Sistem operasi menyediakan tampilan logis untuk penyimpanan informasi
    
    Fungsi manajemen file meliputi: 
    
        1.Membuat dan menghapus file dan direktori
        
        2.Mengelola hak akses file
      
        3.Memetakan file ke penyimpanan sekunder
        
        4.Melakukan pencadangan data ke media penyimpanan yang lebih stabil

---        

1.39 Mass-Storage Management

      Digunakan untuk menyimpan data dalam jangka panjang, biasanya menggunakan hard disk atau penyimpanan sekunder lainnya
      
      Fungsi sistem operasi dalam manajemen penyimpanan meliputi: 

        1.Manajemen ruang kosong
        
        2.Alokasi penyimpanan
        
        3.Penjadwalan disk
        
        4.Partisi dan perlindungan data

---

1.40 Caching

      Konsep penting dalam sistem komputer, diterapkan di berbagai level (hardware, sistem operasi, dan perangkat lunak)
      
      Mekanisme caching: 
        1.Data yang sering digunakan disalin dari penyimpanan yang lebih lambat ke penyimpanan yang lebih cepat
        
        2.Saat data dibutuhkan, sistem pertama-tama mengecek di cache
        
        3.Jika ditemukan di cache, data dapat diakses lebih cepat (cache hit)
        
        4.Jika tidak ada di cache, data diambil dari penyimpanan utama dan disalin ke cache (cache miss)

      Manajemen cache menjadi tantangan desain penting, termasuk menentukan ukuran cache dan kebijakan penggantian data

---

SELESAI
