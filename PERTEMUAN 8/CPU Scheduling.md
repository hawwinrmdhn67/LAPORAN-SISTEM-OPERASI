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

# CPU Scheduling

## Soal 5.17

Consider the following set of processes, with the length of the CPU burst given in milliseconds:

| Process | Burst Time | Priority |
|---------|------------|----------|
| P₁      | 5          | 4        |
| P₂      | 3          | 1        |
| P₃      | 1          | 2        |
| P₄      | 7          | 2        |
| P₅      | 4          | 3        |

The processes are assumed to have arrived in the order P₁, P₂, P₃, P₄, P₅, all at time 0.

A. Draw four Gantt charts that illustrate the execution of these processes using the following scheduling algorithms:
- FCFS
- SJF
- Non-preemptive Priority (a larger priority number implies a higher priority)
- Round Robin (quantum = 2)

B. What is the turnaround time of each process for each of the scheduling algorithms in part a?

C. What is the waiting time of each process for each of these scheduling algorithms?

D. Which of the algorithms results in the minimum average waiting time (over all processes)?

---

## Soal 5.18

The following processes are being scheduled using a preemptive, priority-based, round-robin scheduling algorithm.

| Process | Priority | Burst | Arrival |
|---------|----------|-------|---------|
| P₁      | 8        | 15    | 0       |
| P₂      | 3        | 20    | 0       |
| P₃      | 4        | 20    | 20      |
| P₄      | 4        | 20    | 25      |
| P₅      | 5        | 5     | 45      |
| P₆      | 5        | 15    | 55      |

Each process is assigned a numerical priority, with a higher number indicating a higher relative priority. The scheduler will execute the highest-priority process first. For processes with the same priority, a round-robin scheduler will be used with a time quantum of 10 units. If a process is preempted by a higher-priority process, the preempted process is placed at the end of the queue.

A. Show the scheduling order of the processes using a Gantt chart.

B. What is the turnaround time for each process?

C. What is the waiting time for each process?
