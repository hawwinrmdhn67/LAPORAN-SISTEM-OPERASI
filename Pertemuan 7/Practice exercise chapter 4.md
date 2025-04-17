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

Using Amdahl’s Law, calculate the speedup gain of an application that has a 60 percent parallel component for (a) two processing cores and (b) four processing cores.

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

• 4.2

Does the multithreaded web server described in Section 4.1 exhibit task or data parallelism?

Jawaban : 

    Task Parallelism (Paralelisme Tugas), karena setiap thread menangani task yang berbeda (misal: thread 1 untuk HTTP request, thread 2 untuk
    
    database query)
