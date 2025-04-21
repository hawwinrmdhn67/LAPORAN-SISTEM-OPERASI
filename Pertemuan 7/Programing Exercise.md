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

A. Penerapan thread pada contoh SumTask.java 

Jawaban :

<img src="sumtaskjava.PNG" width="400">

Essay :

SumTask.java merupakan contoh penerapan multithreading di Java menggunakan Fork/Join Framework, yang diperkenalkan sejak Java 7. Program ini dirancang untuk menghitung jumlah elemen dalam array secara paralel, dengan memecah tugas besar menjadi tugas-tugas kecil.

Class SumTask memperluas RecursiveTask<Integer> dan menggunakan metode compute() untuk menghitung total. Jika array lebih besar dari batas tertentu (THRESHOLD), maka tugas akan dibagi dua dan dikerjakan oleh dua sub-task. Masing-masing sub-task akan diproses menggunakan fork() dan hasilnya digabungkan dengan join().

Penggunaan thread di sini tidak dilakukan secara manual (dengan membuat Thread baru), tetapi melalui mekanisme work stealing di ForkJoinPool yang otomatis mengelola thread sesuai kebutuhan.

B. penerapan Thread di Linux (thrd-posix.c) dan 

Jawaban :

<img src="posix.PNG" width="400">

Essay :

thrd-posix.c merupakan implementasi pemrograman paralel menggunakan POSIX Threads (pthreads), yang merupakan standar multithreading pada sistem operasi Unix/Linux. Dalam program ini, setiap thread bertugas menghitung sebagian dari total jumlah integer, lalu hasilnya digabungkan.

Program menggunakan:

- pthread_create() untuk membuat thread.

- pthread_join() untuk menunggu semua thread selesai.

- Argumen fungsi diteruskan melalui pointer.

- Sinkronisasi dilakukan secara eksplisit melalui pengumpulan nilai return dari setiap thread.

C. penerapan thread di Microsoft Windows (thrd-win32.c).

Jawaban :

<img src="win32.PNG" width="500">

Essay :

thrd-win32.c adalah implementasi threading menggunakan Windows API (Win32). Konsepnya mirip dengan versi POSIX, tapi menggunakan fungsi dan struktur khas Windows.

Program menggunakan:

- CreateThread() untuk membuat thread baru.

- WaitForSingleObject() untuk menunggu thread selesai.

- GetExitCodeThread() untuk mengambil hasil akhir dari thread.

---

SELESAI
