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

### PRACTICE EXERCISE CHAPTER 4

• 4.1

Provide three programming examples in which multithreading provides better performance than a single-threaded solution.

Jawaban :

    Web server, video editing, dan game development
    
---

• 4.2

Using Amdahl’s Law, calculate the speedup gain of an application that has a 60 percent parallel component for 

(a) two processing cores and 

(b) four processing cores.

Jawaban :

    Diketahui : 
    
    - Komponen paralel (P) = 60% = 0.6
    - Komponen serial (1-P) = 40% = 0.4
    
    Rumus :
    Speedup = 1 / [(1 - P) + (P/N)]
    
    
    Perhitungan :
    
    a) Dua Core (N=2) :
    Speedup = 1 / [0.4 + (0.6/2)]
    = 1 / (0.4 + 0.3)
    = 1 / 0.7
    ≈ 1.43x
    
    
    b) Empat Core (N=4) :
    Speedup = 1 / [0.4 + (0.6/4)]
    = 1 / (0.4 + 0.15)
    = 1 / 0.55
    ≈ 1.82x

---

• 4.3

Does the multithreaded web server described in Section 4.1 exhibit task or data parallelism?

Jawaban : 

    Task Parallelism (Paralelisme Tugas), karena setiap thread menangani task yang berbeda 
    (misal: thread 1 untuk HTTP request, thread 2 untuk database query)

---

• 4.4

What are two differences between user-level threads and kernel-level threads? Under what circumstances is one type better than the other?

Jawaban : 

    Dua Perbedaan:

    Manajemen
    User-level: Dikelola library (contoh: pthreads) tanpa campur tangan OS.
    Kernel-level: Dikelola langsung oleh OS.
    
    Kinerja
    User-level: Context switch lebih cepat (tidak butuh syscall).
    Kernel-level: Blocking syscall tidak menghentikan seluruh proses.
    
    Keunggulan:
    User-level cocok untuk aplikasi dengan banyak thread ringan (contoh: JVM).
    Kernel-level lebih baik untuk tugas blocking (contoh: I/O intensif).

---

• 4.5

Describe the actions taken by a kernel to context-switch between kernel-level threads.

Jawaban :

    Langkah Kernel:

    1. Simpan state thread aktif (register, PC, stack pointer).
    2. Load state thread baru dari PCB (Process Control Block).
    3. Update scheduling information.
    4. Restore state thread baru ke CPU.

---

• 4.6

What resources are used when a thread is created? How do they differ from those used when a process is created?

Jawaban : 

    Thread:
    Hanya butuh stack, register, dan thread ID (beberapa KB).
    Berbagi memory space, file descriptor, dan resource proses induk.
    
    Proses:
    Butuh memory space terpisah (MB/GB), PCB, dan resource independen.

---

• 4.7

Assume that an operating system maps user-level threads to the kernel using the many-to-many model and that the mapping is done through LWPs. Furthermore, the system allows developers to create real-time threads for use in real-time systems. Is it necessary to bind a real-time thread to an LWP? Explain.

Jawaban :

    Ya, real-time thread harus di-bind ke LWP (Lightweight Process).
    
    Alasan:
    Tanpa binding, thread tidak bisa dapat prioritas real-time dari kernel.
    LWP memastikan thread dijadwalkan secara preemptive untuk memenuhi deadline

---

• 4.8

Provide two programming examples in which multithreading does not provide better performance than a single-threaded solution.

Jawaban : 

    Program Sequential Sederhana
    
    Contoh: Kalkulator yang hanya menjalankan operasi aritmetika dasar (1+2+3+...).
    Alasan: Overhead pembuatan thread lebih besar daripada manfaat paralelisasi.
    
    Aplikasi dengan Banyak Dependency
    
    Contoh: Fibonacci recursive (F(n) = F(n-1) + F(n-2)).
    Alasan: Tiap langkah membutuhkan hasil langkah sebelumnya (tidak bisa diparalelkan).

---

• 4.9

Under what circumstances does a multithreaded solution using multiple kernel threads provide better performance than a single-threaded solution on a single-processor system?

Jawaban : 
    
    Ketika:

    Terdapat operasi I/O-bound (misal: baca/tulis file, network request).
    Thread lain bisa berjalan saat satu thread menunggu I/O (mengurangi idle time CPU).
    
    Contoh:
    Aplikasi web server di single-core masih bisa handle multiple request secara bergantian.

---

• 4.10

Which of the following components of program state are shared across threads in a multithreaded process?

a. Register values

b. Heap memory

c. Global variables

d. Stack memory

Jawaban :

    b. Heap memory (Ya)
    c. Global variables (Ya)
    
    Tidak shared:
    a. Register values (milik masing-masing thread)
    d. Stack memory (setiap thread punya stack sendiri)

---

• 4.11

Can a multithreaded solution using multiple user-level threads achieve better performance on a multiprocessor system than on a single-processor system? Explain.

Jawaban :
    
    Tidak, karena user-level thread tidak diatur oleh kernel, sehingga tidak bisa didistribusikan ke multiple processor.
    Solusi: Gunakan hybrid threading model (contoh: NTPL di Linux).

---

• 4.12

In Chapter 3, we discussed Google's Chrome browser and its practice of opening each new tab in a separate process. Would the same benefits have been achieved if, instead, Chrome had been designed to open each new tab in a separate thread? Explain.

Jawaban :

    Tidak sama, karena:
    
    Keamanan: Isolasi proses mencegah tab crash/exploit mempengaruhi tab lain.
    Stabilitas: Thread dalam proses yang sama berbagi memory space (risiko corruption).

---

• 4.13

Is it possible to have concurrency but not parallelism? Explain.

Jawaban :

    Ya, contoh:
    
    Single-core CPU yang melakukan context-switch antar thread.
    Terlihat bersamaan (concurrent) tapi tidak benar-benar paralel.

---

• 4.14

Using Amdahl's Law, calculate the speedup gain for the following applications:

40 percent parallel with (a) eight processing cores and (b) sixteen processing cores

67 percent parallel with (a) two processing cores and (b) four processing cores

90 percent parallel with (a) four processing cores and (b) eight processing cores

Jawaban :
    
Rumus Amdahl :

<img src="rumus amdahl.png" width="500">

    Perhitungan Speedup Menggunakan Hukum Amdahl
    
    Hasil Perhitungan
    
    1. Aplikasi 40% Paralel (P = 0.4)
    Core (N)	Perhitungan	Speedup
    8	1 / (0.6 + 0.4/8)	≈1.54x
    16	1 / (0.6 + 0.4/16)	≈1.60x
    
    Analisis:
    Speedup terbatas karena 60% kode serial. Penambahan core dari 8→16 hanya memberi peningkatan 0.06x.
    
    3. Aplikasi 67% Paralel (P = 0.67)
    Core (N)	Perhitungan	Speedup
    2	1 / (0.33 + 0.67/2)	≈1.50x
    4	1 / (0.33 + 0.67/4)	≈2.01x
    
    Analisis:
    Peningkatan signifikan (1.5x→2x) karena bagian paralel lebih dominan.
    
    4. Aplikasi 90% Paralel (P = 0.9)
    Core (N)	Perhitungan	Speedup
    4	1 / (0.1 + 0.9/4)	≈3.08x
    8	1 / (0.1 + 0.9/8)	≈4.71x
    
    Analisis:
    Scaling hampir linear karena hanya 10% kode serial

    Jadi :
    
    Speedup maksimum teoritis: 1/(1-P)    
    40% paralel: Maks 1.67x
    90% paralel: Maks 10x
    
    Efektivitas bergantung pada:
    Rasio kode paralel (P)
    Overhead paralelisasi
    
    Untuk P ≥80%, penambahan core memberi dampak signifikan
    
---

• 4.15

Determine if the following problems exhibit task or data parallelism:

• Using a separate thread to generate a thumbnail for each photo in a collection

• Transposing a matrix in parallel

• A networked application where one thread reads from the network and another writes to the network

• The fork-join array summation application described in Section 4.5.2

• The Grand Central Dispatch system

Jawaban : 

    1. Membuat thumbnail untuk setiap foto dalam koleksi
    
        • Data Parallelism
        
        • Alasan: Operasi yang sama (pembuatan thumbnail) diterapkan pada data berbeda (setiap foto).
    
    2.  Transpos matriks secara paralel
    
        • Data Parallelism
        
        • Alasan: Elemen matriks diproses secara terdistribusi (misal: tiap thread mengolah bagian matriks berbeda).
    
    3. Aplikasi jaringan dengan thread baca/tulis terpisah
    
        • Task Parallelism
        
        • Alasan: Thread membaca dan menulis menjalankan task berbeda dengan tujuan berbeda.
    
    4. Fork-join array summation
    
        • Data Parallelism
        
        • Alasan: Array dibagi menjadi bagian-bagian yang dijumlahkan secara paralel.
        
    5. Grand Central Dispatch (GCD) system
    
        • Task Parallelism
        
        • Alasan: GCD mengelola eksekusi task berbeda (bukan data) secara konkuren.    

---

• 4.16

A system with two dual-core processors has four processors available for scheduling. A CPU-intensive application is running on this system. All input is performed at program start-up, when a single file must be opened. Similarly, all output is performed just before the program terminates, when the program results must be written to a single file. Between start-up and termination, the program is entirely CPU-bound. Your task is to improve the performance of this application by multithreading it. The application runs on a system that uses the one-to-one threading model (each user thread maps to a kernel thread).

How many threads will you create to perform the input and output? Explain.

How many threads will you create for the CPU-intensive portion of the application? Explain.

Jawaban : 

    • Input/Output (I/O)
      Jumlah thread: 1 thread untuk input dan 1 untuk output
    
      Penjelasan:
    
        • I/O bersifat sequential (membuka/menulis file tunggal)
        
        • Multithreading tidak mempercepat akses ke file tunggal
        
        • Pembatasan thread menghindari resource contention
    
    • Bagian CPU-Intensif
      Jumlah thread: 4 thread
    
      Penjelasan:
    
        • Sistem memiliki 4 core fisik (2 prosesor dual-core)
        
        • Model one-to-one memastikan tiap thread user mendapat core dedicated
        
        • Lebih dari 4 thread akan menyebabkan overhead context switching

---

