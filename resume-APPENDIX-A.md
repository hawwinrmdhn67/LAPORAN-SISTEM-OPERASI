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

### APPENDIX-A

1. Struktur dan Arsitektur Sistem
   
        Sistem operasi (OS) bertindak sebagai perantara antara pengguna dan perangkat keras. Bagian ini membahas:

             •	Komponen utama OS: Kernel, Shell, sistem manajemen file, dan subsistem lainnya.

             •	Tipe arsitektur OS: 

                  o Monolithic Kernel: Semua layanan OS berjalan dalam satu ruang kernel (contoh: Linux).
     
                  o Microkernel: Memisahkan layanan inti ke dalam modul yang lebih kecil untuk meningkatkan keamanan dan fleksibilitas (contoh: macOS).
     
                  o Layered System: Sistem operasi dibagi menjadi beberapa lapisan fungsional.
     
                  o Hybrid Kernel: Menggabungkan elemen dari monolithic dan microkernel (contoh: Windows NT).

---

2. Manajemen Proses
   
        Bagian ini membahas bagaimana sistem operasi menangani proses, termasuk:
   
             • Definisi proses: Program yang sedang dieksekusi, terdiri dari kode program, data, stack, dan heap.

             • State Diagram: Proses memiliki beberapa status: New, Ready, Running, Waiting, dan Terminated.
   
             • Penjadwalan Proses:
   
                  o Short-Term Scheduler (CPU scheduler) → memilih proses yang akan dieksekusi.
   
                  o Medium-Term Scheduler → mengelola swapping (menghapus proses dari memori sementara).
   
                  o Long-Term Scheduler → mengontrol jumlah proses yang masuk ke sistem.
   
                  o Inter Process Communication (IPC): Proses berkomunikasi menggunakan message passing atau shared memory.

---

3. Manajemen Memori
   
        Sistem operasi harus mengelola memori utama untuk efisiensi dan keamanan.
   
             • Alokasi Memori:
   
                  o Contiguous Allocation: Memori dialokasikan dalam satu blok berurutan.
   
                  o	Non-Contiguous Allocation: Menggunakan paging atau segmentasi.
   
             • Paging:
   
                  o	Memori dibagi menjadi halaman (pages) dengan ukuran tetap.
   
                  o	Menggunakan tabel halaman (page table) untuk menerjemahkan alamat virtual ke fisik.
   
             • Segmentasi:
   
                  o	Memori dibagi menjadi segmen dengan ukuran variabel, sesuai dengan kebutuhan program.
   
                  o	Lebih fleksibel dibandingkan paging tetapi lebih kompleks.
   
             • Virtual Memory:
   
                  o	Memungkinkan eksekusi program yang lebih besar dari RAM fisik.
   
                  o	Menggunakan teknik demand paging dan page replacement algorithms (FIFO, LRU, dll.).


---

4. Sistem I/O dan Manajemen Berkas
   
        Sistem operasi menangani perangkat input/output dan sistem berkas dengan efisien.
   
             • Manajemen I/O: 

                  o Device Driver: Perangkat lunak yang menghubungkan OS dengan perangkat keras.
   
                  o Buffering: Penyimpanan sementara untuk meningkatkan kinerja transfer data.
   
                  o Spooling: Menyimpan data sementara di disk sebelum diproses oleh perangkat lain (misalnya printer).
   
             • Manajemen Berkas:
   
                  o Struktur hirarki sistem file: Direktori, sub-direktori, dan file.
   
                  o Metode alokasi file: Contiguous, Linked, Indexed.
   
                  o Proteksi file menggunakan izin akses (Read, Write, Execute).

---

5. Keamanan dan Proteksi
   
        Keamanan sistem operasi melindungi data dari ancaman eksternal maupun internal.
   
             •	Proteksi Akses:
   
                  o	Menggunakan daftar kontrol akses (Access Control List - ACL).
   
                  o	Model proteksi: Discretionary Access Control (DAC), Mandatory Access Control (MAC).
   
             •	Teknik Keamanan:
   
                  o	Enkripsi untuk melindungi data dalam penyimpanan dan komunikasi.
   
                  o	Firewall untuk menyaring lalu lintas jaringan yang mencurigakan.
   
                  o	Authentication menggunakan kata sandi, sidik jari, atau otentikasi dua faktor.
   
             •	Malware dan Ancaman Keamanan:
   
                  o	Virus, worm, trojan, spyware, dan serangan denial-of-service (DoS).

---

6. Contoh Implementasi dan Studi Kasus
   
        Bagian ini membahas bagaimana konsep di atas diterapkan dalam sistem operasi nyata.
   
             • Linux: 

                  o Menggunakan monolithic kernel dengan modul dinamis.
   
                  o Memiliki sistem berkas berbasis ext4.
   
                  o Open-source dan berbasis UNIX.

             • Windows:
   
                  o Hybrid kernel yang mendukung kompatibilitas aplikasi.
   
                  o GUI berbasis Windows API dan sistem berkas NTFS.
   
                  o Banyak digunakan di dunia bisnis.

             • MacOS:
   
                  o Berbasis microkernel (darwin kernel).
   
                  o Menggunakan sistem berkas Apple File System (APFS).
   
                  o Dikenal karena stabilitas dan keamanannya.

---

SELESAI
