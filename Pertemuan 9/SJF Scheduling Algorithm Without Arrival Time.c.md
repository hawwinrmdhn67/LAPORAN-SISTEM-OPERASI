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

# 1. Buatlah Analisa SJF Scheduling Algorithm Without Arrival Time

## Code :

    #include<stdio.h>
    struct proc
    {
        int no,bt,ct,tat,wt;
    };
    struct proc read(int i)
    {
        struct proc p;
        printf("\nProcess No: %d\n",i);
        p.no=i;
        printf("Enter Burst Time: ");
        scanf("%d",&p.bt);
        return p;
    }
    int main()
    {
        struct proc p[10],tmp;
        float avgtat=0,avgwt=0;
        int n,ct=0;
        printf("<--SJF Scheduling Algorithm Without Arrival Time (Non-Preemptive)-->\n");
        printf("Enter Number of Processes: ");
        scanf("%d",&n);
        for(int i=0;i<n;i++)
            p[i]=read(i+1);
        for(int i=0;i<n-1;i++)
            for(int j=0;j<n-i-1;j++)    
                if(p[j].bt>p[j+1].bt)
                {
    				tmp=p[j];
    				p[j]=p[j+1];
    				p[j+1]=tmp;
                }
        printf("\nProcessNo\tBT\tCT\tTAT\tWT\tRT\n");
        for(int i=0;i<n;i++)
        {
            ct+=p[i].bt;
    		p[i].ct=p[i].tat=ct;
    		avgtat+=p[i].tat;
            p[i].wt=p[i].tat-p[i].bt;
            avgwt+=p[i].wt;
            printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n",p[i].no,p[i].bt,p[i].ct,p[i].tat,p[i].wt,p[i].wt);
        }
        avgtat/=n,avgwt/=n;
        printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
    }

## Outputnya :

<img src="https://github.com/user-attachments/assets/988d6e34-2422-41cd-a613-d23c0a925d54" width="500">

Average Turnaround Time (⟨TAT⟩)
⟨TAT⟩ = (1 + 3 + 6 + 10 + 15) / 5  
⟨TAT⟩ = 35 / 5  
⟨TAT⟩ = **7**

Average Waiting Time (⟨WT⟩)
⟨WT⟩ = (0 + 1 + 3 + 6 + 10) / 5  
⟨WT⟩ = 20 / 5  
⟨WT⟩ = **4**

* **Average TAT** = 7
* **Average WT** = 4

# Analisa menurut saya :

## Struktur Data Proses

```c
struct proc {
    int no;   // Nomor proses
    int bt;   // Burst Time
    int ct;   // Completion Time
    int tat;  // Turnaround Time
    int wt;   // Waiting Time
};
```

Setiap proses direpresentasikan oleh struct `proc` yang menyimpan informasi esensial untuk perhitungan metrik penjadwalan.

## Fungsi Input Proses

```c
struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n", i);
    p.no = i;
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    return p;
}
```

Fungsi `read` meminta input burst time dari pengguna untuk proses ke-i, lalu mengembalikan struct `proc` dengan field `no` dan `bt` terisi.

## Pengurutan (Sorting) Burst Time

```c
for (int i = 0; i < n-1; i++)
    for (int j = 0; j < n-i-1; j++)
        if (p[j].bt > p[j+1].bt) {
            tmp = p[j];
            p[j] = p[j+1];
            p[j+1] = tmp;
        }
```

Menggunakan **bubble sort** untuk mengurutkan array `p[]` berdasarkan `bt` naik. Proses dengan burst time terkecil akan dieksekusi lebih dulu sesuai prinsip SJF.

## Perhitungan Waktu

```c
int ct = 0;
for (int i = 0; i < n; i++) {
    ct += p[i].bt;
    p[i].ct = p[i].tat = ct;
    p[i].wt = p[i].tat - p[i].bt;
    // RT sama dengan WT karena arrival time = 0
    printf("P%d\t%d\t%d\t%d\t%d\t%d\n", p[i].no, p[i].bt, p[i].ct, p[i].tat, p[i].wt, p[i].wt);
}
avgtat /= n;
avgwt /= n;
```

* **`ct`** bertindak sebagai jam berjalan (current time).
* Karena semua proses tiba pada waktu 0, maka:

  * Turnaround Time (TAT) = CT
  * Waiting Time (WT) = TAT – BT
  * Response Time (RT) = WT

---

# 2. Analisa SJF Scheduling Algorithm

## Code :

    #include<stdio.h>
    struct proc
    {
        int no,at,bt,it,ct,tat,wt;
    };
    struct proc read(int i)
    {
        struct proc p;
        printf("\nProcess No: %d\n",i);
        p.no=i;
        printf("Enter Arrival Time: ");
        scanf("%d",&p.at);
        printf("Enter Burst Time: ");
        scanf("%d",&p.bt);
        return p;
    }
    int main()
    {
        int  n,j,min=0;
        float avgtat=0,avgwt=0;
        struct proc p[10],temp;
        printf("<--SJF Scheduling Algorithm (Non-Preemptive)-->\n");
        printf("Enter Number of Processes: ");
        scanf("%d",&n);
        for(int i=0;i<n;i++)
            p[i]=read(i+1);
        for(int i=0;i<n-1;i++)
            for(j=0;j<n-i-1;j++)    
                if(p[j].at>p[j+1].at)
                {
                temp=p[j];
                p[j]=p[j+1];
                p[j+1]=temp;
                }
        for(j=1;j<n&&p[j].at==p[0].at;j++)
            if(p[j].bt<p[min].bt)
                min=j;
        temp=p[0];
        p[0]=p[min];
        p[min]=temp;
        p[0].it=p[0].at;
        p[0].ct=p[0].it+p[0].bt;
        for(int i=1;i<n;i++)
        {
            for(j=i+1,min=i;j<n&&p[j].at<=p[i-1].ct;j++)
                if(p[j].bt<p[min].bt)
                    min=j;
            temp=p[i];
            p[i]=p[min];
            p[min]=temp;
            if(p[i].at<=p[i-1].ct)
                p[i].it=p[i-1].ct;
            else
                p[i].it=p[i].at;
            p[i].ct=p[i].it+p[i].bt;
        }
        printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\tRT\n");
        for(int i=0;i<n;i++)
        {
            p[i].tat=p[i].ct-p[i].at;
            avgtat+=p[i].tat;
            p[i].wt=p[i].tat-p[i].bt;
            avgwt+=p[i].wt;
            printf("P%d\t\t%d\t%d\t%d\t%d\t%d\t%d\n",p[i].no,p[i].at,p[i].bt,p[i].ct,p[i].tat,p[i].wt,p[i].wt);
        }
        avgtat/=n,avgwt/=n;
        printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
    }

## Outputnya :

<img src="https://github.com/user-attachments/assets/eeb3c63d-dbad-4339-984b-54c54bec5cd6" width="400">

Average Turnaround Time (⟨TAT⟩)
⟨TAT⟩ = (20 + 40 + 70 + 110 + 170) / 5  
⟨TAT⟩ = 410 / 5  
⟨TAT⟩ = **82**

Average Waiting Time (⟨WT⟩)
⟨WT⟩ = (0 + 10 + 30 + 50 + 90) / 5  
⟨WT⟩ = 180 / 5  
⟨WT⟩ = **36**

* **Average TAT** = 82
* **Average WT** = 36

# Analisa menurut saya :

## Struktur Data Proses

```c
struct proc {
    int no;   // Nomor proses
    int at;   // Arrival Time
    int bt;   // Burst Time
    int it;   // Initial Time (Start Time)
    int ct;   // Completion Time
    int tat;  // Turnaround Time = CT - AT
    int wt;   // Waiting Time = TAT - BT
};
```

Struktur ini menyimpan informasi setiap proses: nomor, waktu datang, burst time, waktu mulai, selesai, turnaround, dan waiting time.

---

## Fungsi `read()`

```c
struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no=i;
    printf("Enter Arrival Time: ");
    scanf("%d",&p.at);
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    return p;
}
```

Fungsi ini membaca input waktu datang dan burst time dari pengguna, kemudian mengembalikannya dalam bentuk struct.

---

## Sorting Arrival Time

```c
for(int i=0;i<n-1;i++)
    for(j=0;j<n-i-1;j++)    
        if(p[j].at>p[j+1].at)
        {
            temp=p[j];
            p[j]=p[j+1];
            p[j+1]=temp;
        }
```

Sorting proses berdasarkan waktu kedatangan (Arrival Time) menggunakan bubble sort.

---

## Pemilihan Proses SJF

```c
for(j=1;j<n&&p[j].at==p[0].at;j++)
    if(p[j].bt<p[min].bt)
        min=j;
```

Jika dua atau lebih proses datang bersamaan, maka proses dengan burst time terkecil dipilih lebih dulu (Shortest Job First).

---

## Penjadwalan Proses

```c
p[0].it = p[0].at;
p[0].ct = p[0].it + p[0].bt;
```

Proses pertama dimulai pada waktu kedatangannya. Waktu selesai adalah waktu mulai ditambah burst time.

Untuk proses berikutnya:

```c
if(p[i].at <= p[i-1].ct)
    p[i].it = p[i-1].ct;
else
    p[i].it = p[i].at;
p[i].ct = p[i].it + p[i].bt;
```

Jika proses sudah datang, langsung dijalankan. Jika belum, CPU idle menunggu proses datang.

---

## Perhitungan TAT, WT, RT

```c
p[i].tat = p[i].ct - p[i].at;
p[i].wt = p[i].tat - p[i].bt;
```

* **Turnaround Time (TAT)** = CT - AT
* **Waiting Time (WT)** = TAT - BT
* **Response Time (RT)** = Sama dengan WT (karena non-preemptive)

---

# 3. Analisa SRTF Scheduling Algorithm

## Code :

    #include<stdio.h>
    #define MAX 9999
    struct proc
    {
        int no,at,bt,rt,ct,tat,wt;
    };
    struct proc read(int i)
    {
        struct proc p;
        printf("\nProcess No: %d\n",i);
        p.no=i;
        printf("Enter Arrival Time: ");
        scanf("%d",&p.at);
        printf("Enter Burst Time: ");
        scanf("%d",&p.bt);
        p.rt=p.bt;
        return p;
    }
    int main()
    {
        struct proc p[10],temp;
        float avgtat=0,avgwt=0;
        int n,s,remain=0,time;
        printf("<--SRTF Scheduling Algorithm (Preemptive)-->\n");
        printf("Enter Number of Processes: ");
        scanf("%d",&n);
        for(int i=0;i<n;i++)
            p[i]=read(i+1);
        for(int i=0;i<n-1;i++)
            for(int j=0;j<n-i-1;j++)    
                if(p[j].at>p[j+1].at)
                {
                temp=p[j];
                p[j]=p[j+1];
                p[j+1]=temp;
                }
        printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\n");
        p[9].rt=MAX;
        for(time=0;remain!=n;time++)
        {
            s=9;
            for(int i=0;i<n;i++)
                if(p[i].at<=time&&p[i].rt<p[s].rt&&p[i].rt>0)
                    s=i;
            p[s].rt--;
            if(p[s].rt==0)
            {
                remain++;
                p[s].ct=time+1;
                p[s].tat=p[s].ct-p[s].at;
                avgtat+=p[s].tat;
                p[s].wt=p[s].tat-p[s].bt;
                avgwt+=p[s].wt;
                printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n",p[s].no,p[s].at,p[s].bt,p[s].ct,p[s].tat,p[s].wt);
            }
        }
        avgtat/=n,avgwt/=n;
        printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
    }

## Outputnya :

<img src="https://github.com/user-attachments/assets/5d104d81-fc56-4de7-abce-b4ab89e53d52" width="400">

Average Turnaround Time (⟨TAT⟩)
⟨TAT⟩ = (35 + 75 + 145 + 235 + 435) / 5  
⟨TAT⟩ = 925 / 5  
⟨TAT⟩ = **185**

Average Waiting Time (⟨WT⟩)
⟨WT⟩ = (0 + 5 + 55 + 125 + 135) / 5  
⟨WT⟩ = 320 / 5  
⟨WT⟩ = **64**

* **Average TAT** = 185
* **Average WT** = 64

# Analisa menurut saya :

## Struktur Data Proses

```c
struct proc {
    int no;   // Nomor proses
    int at;   // Arrival Time
    int bt;   // Burst Time
    int rt;   // Remaining Time
    int ct;   // Completion Time
    int tat;  // Turnaround Time = CT - AT
    int wt;   // Waiting Time = TAT - BT
};
```

## Sorting Berdasarkan Arrival Time

    for (int i = 0; i < n-1; i++)
        for (int j = 0; j < n-i-1; j++)
            if (p[j].at > p[j+1].at) {
                temp = p[j];
                p[j] = p[j+1];
                p[j+1] = temp;
            }

Seluruh proses diurutkan naik berdasarkan at (arrival time) menggunakan bubble sort. Hal ini memastikan bahwa saat loop waktu berjalan, proses yang sudah “datang” (tidak melebihi time) dapat dipertimbangkan untuk dieksekusi.

## Penjadwalan Preemptive (SRTF)

    p[9].rt = MAX;  // Inisialisasi sentinel untuk membandingkan remaining time
    
    for (time = 0; remain != n; time++) {
        // Pilih proses dengan remaining time (rt) terkecil yang sudah tiba dan belum selesai
        s = 9;  
        for (int i = 0; i < n; i++)
            if (p[i].at <= time && p[i].rt < p[s].rt && p[i].rt > 0)
                s = i;
    
        // Eksekusi selama 1 unit waktu
        p[s].rt--;
    
        // Bila proses selesai (rt == 0), hitung metrik
        if (p[s].rt == 0) {
            remain++;
            p[s].ct  = time + 1;
            p[s].tat = p[s].ct - p[s].at;
            p[s].wt  = p[s].tat - p[s].bt;
            avgtat += p[s].tat;
            avgwt  += p[s].wt;
            printf("P%d\t%d\t%d\t%d\t%d\t%d\n",
                   p[s].no, p[s].at, p[s].bt, p[s].ct, p[s].tat, p[s].wt);
        }
    }

## Penjadwalan berjalan dalam loop waktu satuan (time++) hingga semua proses selesai (remain == n)

1. Sentinel (p[9].rt = MAX): Digunakan untuk memudahkan pemilihan proses pertama kali dalam setiap iterasi.

2. Pemilihan Proses: Cari indeks s dengan rt terkecil di antara proses yang at ≤ time dan rt > 0.

3. Preemption: Karena cek dilakukan tiap unit waktu, bila ada proses baru datang dengan rt lebih kecil, eksekusi berpindah (preemptive).

4. Penyelesaian Proses: Saat rt turun ke 0, proses dianggap selesai pada time + 1.

---

SELESAI
