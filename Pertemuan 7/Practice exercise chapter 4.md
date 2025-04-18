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

• 4.17

Consider the following code segment:

    pid_t pid;
    pid = fork();
    if (pid == 0) { /* child process */
        fork();
        thread.create( . . .);
    }
    fork();

a. How many unique processes are created?

b. How many unique threads are created?

Jawaban :

    a. How many unique processes are created?
    
    Penjelasan :
    
    • Fork 1 membuat 1 proses anak (total proses sekarang: 2).
    
    • Hanya proses anak (pid == 0) yang menjalankan Fork 2, menghasilkan 1 proses tambahan (total: 3).
    
    • Fork 3 dijalankan oleh semua proses yang ada (3 proses), sehingga masing-masing membuat 1 proses baru (total akhir: 3 + 3 = 6).
    
      • Namun, proses "utama" (parent awal) sudah dihitung, jadi proses unik yang baru dibuat adalah 5 (6 total dikurangi parent awal).

    b. How many unique threads are created?
    
    Penjelasan :
    
    • thread_create() hanya dipanggil oleh proses anak hasil Fork 1 (setelah Fork 2).

    • Hanya 1 thread yang dibuat, dan thread ini berbagi alamat memori dengan proses anak tersebut.

---

• 4.18

As described in Section 4.7.2, Linux does not distinguish between processes and threads. Instead, Linux treats both in the same way, allowing a task to be more akin to a process or a thread depending on the set of flags passed to the clone() system call. However, other operating systems, such as Windows, treat processes and threads differently. Typically, such systems use a notation in which the data structure for a process contains pointers to the separate threads belonging to the process. Contrast these two approaches for modeling processes and threads within the kernel.

Jawaban : 

| **Fitur**               | **Linux (`clone()`)**                              | **Windows (Proses/Thread Terpisah)**          |
|-------------------------|---------------------------------------------------|---------------------------------------------|
| **Representasi Kernel** | Satu `task_struct` untuk keduanya                 | `EPROCESS` (proses) + `ETHREAD` (thread)    |
| **System Call Pembuatan**| `clone()` dengan flag (misal `CLONE_VM` untuk thread)| `CreateProcess()` (proses) + `CreateThread()` |
| **Berbagi Sumber Daya** | Fleksibel (memori, FD, dll. berdasarkan flag)     | Thread berbagi memori proses; proses terisolasi |
| **Overhead**            | Rendah (tidak ada struktur tambahan)              | Lebih tinggi (pemisahan eksplisit)          |
| **Contoh Penggunaan**   | Container Docker (proses ringan)                  | Aplikasi multithreaded (misal Chrome)       |

---

• 4.19

The program shown in Figure 4.23 uses the Pthreads API. What would be the output from the program at LINE C and LINE P?

Jawaban :

    #include <pthread.h>
    #include <stdio.h>
    
    int value = 0;
    void *runner(void *param); /* the thread */
    
    int main(int argc, char *argv[]) {
        pid_t pid;
        pthread_t tid;
        pthread_attr_t attr;
    
        pid = fork();
    
        if (pid == 0) { /* child process */
            pthread_attr_init(&attr);
            pthread_create(&tid, &attr, runner, NULL);
            pthread_join(tid, NULL);
            printf("CHILD: value = %d", value); /* LINE C */
        }
        else if (pid > 0) { /* parent process */
            wait(NULL);
            printf("PARENT: value = %d", value); /* LINE P */
        }
    }
    
    void *runner(void *param) {
        value = 5;
        pthread_exit(0);
    }

Outputnya :

CHILD: value = 5

PARENT: value = 0

---

• 4.20

Consider a multicore system and a multithreaded program using the many-to-many threading model, where the number of user-level threads exceeds the number of processing cores. Discuss the performance implications of:

a. The number of kernel threads is less than the number of cores.

b. The number of kernel threads equals the number of cores.

c. The number of kernel threads is greater than the number of cores but less than user-level threads.

Jawaban :

    a. Jumlah Thread Kernel < Jumlah Core
    
    Contoh :
    • 8 core
    • 4 thread kernel
    • 100 thread user
    
    Implikasi :
    • Pemanfaatan core tidak maksimal.
    • Hanya 4 ULT yang dapat berjalan sekaligus, meskipun ada 8 core.
    • Sebagian core akan idle, menyebabkan pemborosan sumber daya.
    • Banyak ULT harus menunggu KLT tersedia, meningkatkan latensi.
    
    Dampak Performa :
    • Efisiensi rendah
    • Throughput kecil
    • Tingkat responsivitas buruk
    • Potensi starvation (kelaparan thread)
    
    b. Jumlah Thread Kernel = Jumlah Core
    
    Contoh :
    • 8 core
    • 8 thread kernel
    • 100 thread user
    
    Implikasi :
    • Pemanfaatan core optimal — semua core dapat menjalankan 1 KLT.
    • ULT dapat dijadwalkan secara bergantian tanpa menghambat core.
    • Sistem dapat mengelola eksekusi ULT dengan efisien.
    
    Dampak Performa :
    • Efisiensi tinggi
    • Throughput maksimal
    • Responsivitas baik
    • Beban sistem stabil
    
    c. Jumlah Thread Kernel > Jumlah Core tapi < Jumlah Thread User
    
    Contoh :
    • 8 core
    • 12 thread kernel
    • 100 thread user
    
    Implikasi :
    • Lebih banyak ULT bisa dijalankan secara paralel, meskipun hanya 8 yang bisa aktif sekaligus.
    • Kernel perlu melakukan context switching antar KLT, menyebabkan overhead kecil.
    • Namun sistem lebih fleksibel dibanding skenario (a).
    
    Dampak Performa :
    • Efisiensi masih baik
    • Overhead switching meningkat, tapi masih dalam batas wajar
    • Responsivitas lebih baik dari (a), meski tidak seoptimal (b)
    
    | Kondisi | Efisiensi CPU | Throughput | Responsivitas |
    |--------|----------------|-------------|----------------|
    | a. KLT < Core | Rendah | Rendah | Buruk |
    | b. KLT = Core | Optimal | Tinggi | Baik |
    | c. KLT > Core tapi < ULT | Menengah-Tinggi | Cukup Baik | Lebih Baik dari (a) 
    
    Semakin besar jumlah user-level threads, semakin penting manajemen thread pool dan strategi load balancing untuk menjaga performa sistem tetap stabil.

---

• 4.21

Pthreads provides an API for managing thread cancellation. The pthread_setcancelstate() function is used to set the cancellation state. Its prototype appears as follows

    pthread_setcancelstate(int state, int *oldstate);

The two possible values for the state are:

• PTHREAD_CANCEL_ENABLE

• PTHREAD_CANCEL_DISABLE

Using the code segment shown in Figure 4.24, provide examples of two operations that would be suitable to perform between the calls to disable and enable thread cancellation.

    int oldstate;
    pthread_setcancelstate(PTHREAD_CANCEL_DISABLE, &oldstate);
    /* What operations would be performed here? */
    pthread_setcancelstate(PTHREAD_CANCEL_ENABLE, &oldstate);

Jawaban :

Manajemen Pembatalan Thread dengan `pthread_setcancelstate()`

Pthreads menyediakan API untuk mengatur pembatalan thread (thread cancellation), salah satunya melalui fungsi:

    int pthread_setcancelstate(int state, int *oldstate);

Parameter state dapat bernilai:

• PTHREAD_CANCEL_ENABLE : mengaktifkan pembatalan thread

• PTHREAD_CANCEL_DISABLE : menonaktifkan pembatalan thread sementara

Contoh Operasi yang Cocok Saat Pembatalan Dinonaktifkan

• PTHREAD_CANCEL_DISABLE

    pthread_mutex_lock(&mutex);
    shared_counter += 1;
    pthread_mutex_unlock(&mutex);

- Jika thread dibatalkan saat memodifikasi data bersama, dapat menyebabkan data race atau inkonsistensi data.

- Menonaktifkan pembatalan mencegah thread keluar sebelum menyelesaikan modifikasi dengan aman.

• PTHREAD_CANCEL_ENABLE

    char *buffer = malloc(1024);
    if (buffer != NULL) {
        memset(buffer, 0, 1024);
        // Lanjutkan penggunaan buffer...
    }

- Jika thread dibatalkan setelah malloc() tapi sebelum free(), akan terjadi memory leak.

- Pembatalan harus dinonaktifkan selama manajemen memori.

---

• 4.22

Write a multithreaded program that calculates various statistical values for a list of numbers. This program will be passed a series of numbers on the command line and will then create three separate worker threads. One thread will determine the average of the numbers, the second will determine the maximum value, and the third will determine the minimum value. For example, suppose your program is passed the integers

The program will report

- The average value is 82

- The minimum value is 72

- The maximum value is 95

The variables representing the average, minimum, and maximum values will be stored globally. The worker threads will set these values, and the parent thread will output the values once the workers have exited. (We could obviously expand this program by creating additional threads that determine other statistical values, such as median and standard deviation.)

Jawaban : 

Program Multithread untuk Menghitung Statistik

    #include <stdio.h>
    #include <stdlib.h>
    #include <pthread.h>
    
    // Variabel global untuk menyimpan hasil
    double average = 0;
    int minimum = 0;
    int maximum = 0;
    
    // Struktur untuk passing data ke thread
    typedef struct {
        int *numbers;
        int count;
    } ThreadData;
    
    // Fungsi untuk menghitung rata-rata
    void *calculate_average(void *arg) {
        ThreadData *data = (ThreadData *)arg;
        int sum = 0;
        for (int i = 0; i < data->count; i++) {
            sum += data->numbers[i];
        }
        average = (double)sum / data->count;
        pthread_exit(NULL);
    }
    
    // Fungsi untuk mencari nilai minimum
    void *calculate_minimum(void *arg) {
        ThreadData *data = (ThreadData *)arg;
        minimum = data->numbers[0];
        for (int i = 1; i < data->count; i++) {
            if (data->numbers[i] < minimum) {
                minimum = data->numbers[i];
            }
        }
        pthread_exit(NULL);
    }
    
    // Fungsi untuk mencari nilai maksimum
    void *calculate_maximum(void *arg) {
        ThreadData *data = (ThreadData *)arg;
        maximum = data->numbers[0];
        for (int i = 1; i < data->count; i++) {
            if (data->numbers[i] > maximum) {
                maximum = data->numbers[i];
            }
        }
        pthread_exit(NULL);
    }
    
    int main(int argc, char *argv[]) {
        if (argc < 2) {
            printf("Usage: %s <number1> <number2> ... <numberN>\n", argv[0]);
            return 1;
        }
    
        int *numbers = malloc((argc - 1) * sizeof(int));
        for (int i = 1; i < argc; i++) {
            numbers[i - 1] = atoi(argv[i]);
        }
    
        ThreadData data = {numbers, argc - 1};
    
        // Buat thread untuk masing-masing tugas
        pthread_t threads[3];
        pthread_create(&threads[0], NULL, calculate_average, &data);
        pthread_create(&threads[1], NULL, calculate_minimum, &data);
        pthread_create(&threads[2], NULL, calculate_maximum, &data);
    
        // Tunggu semua thread selesai
        for (int i = 0; i < 3; i++) {
            pthread_join(threads[i], NULL);
        }
    
        // Cetak hasil
        printf("The average value is %.0f\n", average);
        printf("The minimum value is %d\n", minimum);
        printf("The maximum value is %d\n", maximum);
    
        free(numbers);
        return 0;
    }
Penjelasan :

Variabel Global:

- average, minimum, maximum menyimpan hasil perhitungan.

Struktur ThreadData:

- Menyimpan pointer ke array angka (numbers) dan jumlah elemen (count).

Fungsi Thread:

- calculate_average: Menghitung rata-rata.

- calculate_minimum: Mencari nilai terkecil.

- calculate_maximum: Mencari nilai terbesar.

Main Program:

- Parsing input dari command line.

- Membuat 3 thread terpisah untuk masing-masing perhitungan.

- Menunggu thread selesai dengan pthread_join.

- Mencetak hasil dan membersihkan memori

• Thread Safety: Variabel global diakses secara eksklusif oleh masing-masing thread (tidak ada race condition).

• Extensibility: Program bisa dikembangkan untuk menghitung statistik lain (median, standar deviasi) dengan menambah thread baru.

---

• 4.23

Write a multithreaded program that outputs prime numbers. This program should work as follows: The user will run the program and will enter a number on the command line. The program will then create a separate thread that outputs all the prime numbers less than or equal to the number entered by the user.

Jawaban :

Program Multithread untuk Mencetak Bilangan Prima

    #include <stdio.h>
    #include <stdlib.h>
    #include <pthread.h>
    #include <stdbool.h>
    
    // Fungsi untuk mengecek apakah suatu bilangan prima
    bool is_prime(int num) {
        if (num <= 1) return false;
        if (num == 2) return true;
        if (num % 2 == 0) return false;
        
        for (int i = 3; i * i <= num; i += 2) {
            if (num % i == 0) {
                return false;
            }
        }
        return true;
    }
    
    // Fungsi yang dijalankan oleh thread untuk mencetak bilangan prima
    void *print_primes(void *arg) {
        int limit = *((int *)arg);
        printf("Bilangan prima <= %d:\n", limit);
        
        for (int i = 2; i <= limit; i++) {
            if (is_prime(i)) {
                printf("%d ", i);
            }
        }
        printf("\n");
        
        pthread_exit(NULL);
    }
    
    int main(int argc, char *argv[]) {
        if (argc != 2) {
            printf("Usage: %s <angka>\n", argv[0]);
            return 1;
        }
    
        int limit = atoi(argv[1]);
        if (limit < 2) {
            printf("Masukkan angka >= 2\n");
            return 1;
        }
    
        pthread_t prime_thread;
        pthread_create(&prime_thread, NULL, print_primes, &limit);
        pthread_join(prime_thread, NULL);
    
        return 0;
    }

Penjelasan :

Fungsi is_prime():

- Mengecek apakah suatu bilangan prima dengan:

- Bilangan ≤ 1 bukan prima

- Bilangan 2 adalah prima

- Bilangan genap > 2 bukan prima

- Pengecekan pembagi hingga √num untuk efisiensi

- Fungsi Thread print_primes():

- Menerima argumen limit (batas atas)

- Mencetak semua bilangan prima dari 2 hingga limit

Main Program:

- Validasi input (harus 1 angka ≥ 2)

- Membuat thread khusus untuk mencetak bilangan prima

- Menunggu thread selesai dengan pthread_join()

---

• 4.24

An interesting way of calculating π is to use a technique known as Monte Carlo, which involves randomization. This technique works as follows:
Suppose you have a circle inscribed within a square, as shown in Figure 4. Assume that the radius of this circle is 1/3.

First, generate a series of random points as simple (x,y) coordinates. These points must fall within the Cartesian coordinates that bound the square. Of the total number of random points that are generated, some will occur within the circle.

Next, estimate π by performing the following calculation:

<img src="monte carlo.png" width="500">

Write a multithreaded version of this algorithm that creates a separate thread to generate a number of random points. The thread will count the number of points that occur within the circle and store that result in a global variable. When this thread has exited, the parent thread will calculate and output the estimated value of π. It is worth experimenting with the number of random points generated. As a general rule, the greater the number of points, the closer the approximation to π.

<img src="monte carlo calculating.png" width="400">

In the source-code download for this text, you will find a sample program that provides a technique for generating random numbers, as well as determining if the random (x,y) point occurs within the circle.

Readers interested in the details of the Monte Carlo method for estimating π should consult the bibliography at the end of this chapter. In Chapter 6, we modify this exercise using relevant material from that chapter.

Jawaban :

Program Multithread untuk Menghitung π dengan Metode Monte Carlo

    #include <stdio.h>
    #include <stdlib.h>
    #include <pthread.h>
    #include <time.h>
    #include <math.h>
    
    #define RADIUS (1.0/3.0)  // Jari-jari lingkaran = 1/3
    
    int total_points = 0;      // Jumlah total titik
    int points_in_circle = 0;  // Jumlah titik dalam lingkaran (global variable)
    
    // Fungsi thread untuk menghasilkan titik acak
    void *generate_points(void *arg) {
        int n = *((int *)arg);
        unsigned int seed = time(NULL) ^ pthread_self(); // Seed unik untuk tiap thread
        
        for (int i = 0; i < n; i++) {
            double x = (double)rand_r(&seed) / RAND_MAX * 2 * RADIUS - RADIUS;
            double y = (double)rand_r(&seed) / RAND_MAX * 2 * RADIUS - RADIUS;
            
            // Cek apakah titik berada dalam lingkaran (x² + y² ≤ r²)
            if (x*x + y*y <= RADIUS*RADIUS) {
                points_in_circle++;
            }
        }
        pthread_exit(NULL);
    }
    
    int main(int argc, char *argv[]) {
        if (argc != 2) {
            printf("Usage: %s <jumlah_titik>\n", argv[0]);
            return 1;
        }
    
        total_points = atoi(argv[1]);
        if (total_points <= 0) {
            printf("Jumlah titik harus > 0\n");
            return 1;
        }
    
        pthread_t monte_carlo_thread;
        pthread_create(&monte_carlo_thread, NULL, generate_points, &total_points);
        pthread_join(monte_carlo_thread, NULL);
    
        // Hitung estimasi π
        double pi_estimate = 6.0 * points_in_circle / total_points;
        printf("Estimasi π = %f (dengan %d titik)\n", pi_estimate, total_points);
    
        return 0;
    }

Penjelasan :

Thread Utama (main)

- Membaca jumlah titik dari input command line

- Membuat thread pekerja (monte_carlo_thread) untuk memproses titik

- Menunggu thread selesai (pthread_join)

- Menghitung dan mencetak estimasi π

Thread Pekerja (generate_points)

- Membuat titik-titik acak di dalam area persegi

- Menghitung titik yang jatuh di dalam lingkaran (x² + y² ≤ r²)

- Menyimpan hasil di variabel global points_in_circle

---

• 4.25

Repeat Exercise 4.24, but instead of using a separate thread to generate random points, use OpenMP to parallelize the generation of points. Be careful not to place the calculation of π in the parallel region, since you want to calculate π only once.

Jawaban :

Program Monte Carlo dengan OpenMP

    #include <stdio.h>
    #include <stdlib.h>
    #include <omp.h>
    #include <math.h>
    
    #define RADIUS (1.0/3.0)
    
    int main(int argc, char *argv[]) {
        if (argc != 2) {
            printf("Penggunaan: %s <jumlah_titik>\n", argv[0]);
            return 1;
        }
    
        int total_points = atoi(argv[1]);
        int points_in_circle = 0;
    
        #pragma omp parallel for reduction(+:points_in_circle)
        for (int i = 0; i < total_points; i++) {
            double x = (double)rand() / RAND_MAX * 2 * RADIUS - RADIUS;
            double y = (double)rand() / RAND_MAX * 2 * RADIUS - RADIUS;
            if (x*x + y*y <= RADIUS*RADIUS) {
                points_in_circle++;
            }
        }
    
        double pi_estimate = 6.0 * points_in_circle / total_points;
        printf("Estimasi π = %f\n", pi_estimate);
    
        return 0;
    }

Penjelasan :

- #pragma omp parallel for membagi loop ke beberapa thread.

- reduction(+:points_in_circle) menggabungkan hasil dari semua thread.

- Kompilasi: gcc -fopenmp monte_carlo_omp.c -o monte_carlo_omp

---

• 4.26

Modify the socket-based date server (Figure 3.27) in Chapter 3 so that the server services each client request in a separate thread.

Jawaban :

Program Server Tanggal Multithread

    #include <stdio.h>
    #include <stdlib.h>
    #include <pthread.h>
    #include <unistd.h>
    #include <sys/socket.h>
    #include <netinet/in.h>
    #include <time.h>
    
    void *handle_client(void *arg) {
        int client_socket = *((int *)arg);
        time_t rawtime;
        time(&rawtime);
        char *response = ctime(&rawtime);
        send(client_socket, response, strlen(response), 0);
        close(client_socket);
        pthread_exit(NULL);
    }
    
    int main() {
        int server_socket = socket(AF_INET, SOCK_STREAM, 0);
        struct sockaddr_in server_addr = {
            .sin_family = AF_INET,
            .sin_port = htons(8080),
            .sin_addr.s_addr = INADDR_ANY
        };
    
        bind(server_socket, (struct sockaddr *)&server_addr, sizeof(server_addr));
        listen(server_socket, 5);
    
        while (1) {
            int client_socket = accept(server_socket, NULL, NULL);
            pthread_t thread;
            pthread_create(&thread, NULL, handle_client, &client_socket);
            pthread_detach(thread); // Agar thread cleanup otomatis
        }
    
        return 0;
    }

Penjelasan :

- Setiap koneksi klien ditangani oleh thread baru.

- pthread_detach mencegah memory leak.

- Kompilasi: gcc server.c -o server -lpthread

---

• 4.27

The Fibonacci sequence is the series of numbers 0,1,1,2,3,5,8,... Formally, it can be expressed as:

