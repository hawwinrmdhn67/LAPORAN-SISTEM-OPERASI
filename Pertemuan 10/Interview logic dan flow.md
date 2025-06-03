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

## Flow dan logic SJF dan SRTF Scheduling (S10-Chapter-05)

---

### 1. SJF (Shortest Job First) Without Arrival Time

SJF tanpa arrival time berarti semua proses dianggap datang bersamaan (misalnya pada waktu 0). Algoritma akan mengeksekusi proses dengan burst time (waktu eksekusi CPU) terpendek lebih dahulu.

**Contoh Kasus (Practice Exercise 5.3):**

```
Process  Burst Time
P1       6
P2       8
P3       7
P4       3
```

* Urutan eksekusi: P4 → P1 → P3 → P2

**Perhitungan Waktu:**

| Process | Burst Time | Waiting Time (WT) | Turnaround Time (TAT) |
| ------- | ---------- | ----------------- | --------------------- |
| P4      | 3          | 0                 | 3                     |
| P1      | 6          | 3                 | 9                     |
| P3      | 7          | 9                 | 16                    |
| P2      | 8          | 16                | 24                    |

**Total Waktu Eksekusi:** 24 satuan waktu
**Total Burst Time:** 3 + 6 + 7 + 8 = 24 satuan waktu

**Flow Logic Program:**

1. Simpan semua proses dan burst time dalam array/list.
2. Urutkan proses berdasarkan burst time terkecil.
3. Hitung waiting time dan turnaround time:

   * Waiting Time proses pertama = 0
   * Waiting Time proses ke-i = WT\[i-1] + BT\[i-1]
   * Turnaround Time = WT + BT

---

### 2. SJF With Arrival Time (Non-Preemptive)

SJF mempertimbangkan waktu kedatangan. Proses dengan burst time terkecil **di antara proses yang sudah tiba** yang akan diproses dulu.

**Contoh Kasus (Practice Exercise 5.4):**

```
Process  Arrival Time  Burst Time
P1       0             8
P2       1             4
P3       2             9
P4       3             5
```

* Urutan eksekusi: P1 → P2 → P4 → P3

**Perhitungan Waktu:**

| Process | Arrival Time | Burst Time | Start Time | Completion Time | Waiting Time | Turnaround Time |
| ------- | ------------ | ---------- | ---------- | --------------- | ------------ | --------------- |
| P1      | 0            | 8          | 0          | 8               | 0            | 8               |
| P2      | 1            | 4          | 8          | 12              | 7            | 11              |
| P4      | 3            | 5          | 12         | 17              | 9            | 14              |
| P3      | 2            | 9          | 17         | 26              | 15           | 24              |

**Total Waktu Eksekusi:** 26 satuan waktu
**Total Burst Time:** 8 + 4 + 5 + 9 = 26 satuan waktu

**Flow Logic Program:**

1. Simpan semua proses dengan arrival dan burst time.
2. Simulasikan waktu mulai dari 0.
3. Setiap waktu:

   * Pilih proses yang sudah datang dan memiliki burst time terpendek.
   * Jalankan hingga selesai (non-preemptive).
4. Hitung waiting time dan turnaround time.

---

### 3. SRTF (Shortest Remaining Time First - Preemptive SJF)

Versi preemptive dari SJF. Jika proses baru datang dan memiliki burst time lebih pendek dari sisa waktu proses yang sedang berjalan, maka proses baru akan **menghentikan** proses sebelumnya.

**Contoh Kasus (Practice Exercise 5.6):**

```
Process  Arrival Time  Burst Time
P1       0             8
P2       1             4
P3       2             9
P4       3             5
```

* P2 datang saat P1 sedang jalan, dan karena burst P2 < sisa waktu P1, maka P2 menggantikan P1.

**Perhitungan Singkat (Gantt Chart Simulasi):**

```
0   1   5   10  17  26
| P1 | P2 | P4 | P1 | P3 |
```

| Process | Arrival Time | Burst Time | Completion Time | Turnaround Time | Waiting Time |
| ------- | ------------ | ---------- | --------------- | --------------- | ------------ |
| P1      | 0            | 8          | 17              | 17              | 9            |
| P2      | 1            | 4          | 5               | 4               | 0            |
| P3      | 2            | 9          | 26              | 24              | 15           |
| P4      | 3            | 5          | 10              | 7               | 2            |

**Total Waktu Eksekusi:** 26 satuan waktu
**Total Burst Time:** 8 + 4 + 9 + 5 = 26 satuan waktu

**Flow Logic Program:**

1. Simpan proses dengan arrival dan burst time.
2. Pada setiap satuan waktu:

   * Cek proses yang sudah datang.
   * Pilih proses dengan **sisa waktu terkecil**.
   * Jalankan 1 unit waktu.
   * Jika ada proses baru yang lebih pendek, preempt.
3. Ulangi sampai semua proses selesai.
4. Hitung waktu selesai, waiting time, dan turnaround time.

---

### Perbedaan SJF with arrival, SJF without arrival, dan SRTF:

  * SJF without arrival = semua proses datang bersamaan.
  * SJF with arrival = pilih burst terkecil di antara proses yang sudah datang.
  * SRTF = proses bisa diinterupsi oleh proses yang lebih pendek.

---

SELESAI
