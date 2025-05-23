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

SELESAI
