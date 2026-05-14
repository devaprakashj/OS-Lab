# Exercise 3: Implementation of CPU Scheduling Algorithms

## 🎯 Aim
To write and execute a C program to implement basic CPU scheduling algorithms such as First Come First Serve (FCFS), Shortest Job First (SJF), Priority Scheduling, and Round Robin Scheduling, and to calculate waiting time and turnaround time for each process.

## 📝 Procedure

**Common Setup Step:**
1. Open the Linux terminal.
2. It's recommended to do this in a separate folder. Type: `mkdir Ex_03` and then `cd Ex_03`.

**Step-by-Step Execution for Each Algorithm:**

**1. To Run FCFS:**
- Create file: `gedit fcfs.c` (or `vim fcfs.c`)
- Paste the FCFS code and Save.
- Compile: `gcc fcfs.c -o fcfs`
- Run: `./fcfs`

**2. To Run SJF:**
- Create file: `gedit sjf.c` (or `vim sjf.c`)
- Paste the SJF code and Save.
- Compile: `gcc sjf.c -o sjf`
- Run: `./sjf`

**3. To Run Priority Scheduling:**
- Create file: `gedit priority.c` (or `vim priority.c`)
- Paste the Priority code and Save.
- Compile: `gcc priority.c -o priority`
- Run: `./priority`

**4. To Run Round Robin:**
- Create file: `gedit rr.c` (or `vim rr.c`)
- Paste the Round Robin code and Save.
- Compile: `gcc rr.c -o rr`
- Run: `./rr`

---

## 💻 Implementation Codes

### 1. FCFS (First Come First Serve)
```c
#include <stdio.h>

int main() {
    int n, i;
    int bt[20], wt[20], tat[20];
    
    printf("Enter number of processes: ");
    scanf("%d", &n);
    
    for(i = 0; i < n; i++) {
        printf("Enter Burst Time for P%d: ", i + 1);
        scanf("%d", &bt[i]);
    }
    
    wt[0] = 0;
    for(i = 1; i < n; i++)
        wt[i] = wt[i - 1] + bt[i - 1];
        
    for(i = 0; i < n; i++)
        tat[i] = wt[i] + bt[i];
        
    printf("\nProcess\tBT\tWT\tTAT\n");
    for(i = 0; i < n; i++)
        printf("P%d\t%d\t%d\t%d\n", i + 1, bt[i], wt[i], tat[i]);
        
    return 0;
}
```

### 2. SJF (Shortest Job First)
```c
#include <stdio.h>

int main() {
    int bt[20], p[20], wt[20], tat[20], n, i, j, temp;
    
    printf("Enter number of processes: ");
    scanf("%d", &n);
    
    for(i = 0; i < n; i++) {
        printf("Enter Burst Time for P%d: ", i + 1);
        scanf("%d", &bt[i]);
        p[i] = i + 1;
    }
    
    for(i = 0; i < n; i++) {
        for(j = i + 1; j < n; j++) {
            if(bt[i] > bt[j]) {
                temp = bt[i]; bt[i] = bt[j]; bt[j] = temp;
                temp = p[i]; p[i] = p[j]; p[j] = temp;
            }
        }
    }
    
    wt[0] = 0;
    for(i = 1; i < n; i++)
        wt[i] = wt[i - 1] + bt[i - 1];
        
    for(i = 0; i < n; i++)
        tat[i] = wt[i] + bt[i];
        
    printf("\nProcess\tBT\tWT\tTAT\n");
    for(i = 0; i < n; i++)
        printf("P%d\t%d\t%d\t%d\n", p[i], bt[i], wt[i], tat[i]);
        
    return 0;
}
```

### 3. Priority Scheduling
```c
#include <stdio.h>

int main() {
    int bt[20], p[20], wt[20], tat[20], pr[20];
    int n, i, j, temp;
    
    printf("Enter number of processes: ");
    scanf("%d", &n);
    
    for(i = 0; i < n; i++) {
        printf("Burst time for P%d: ", i + 1);
        scanf("%d", &bt[i]);
        printf("Priority for P%d: ", i + 1);
        scanf("%d", &pr[i]);
        p[i] = i + 1;
    }
    
    for(i = 0; i < n; i++) {
        for(j = i + 1; j < n; j++) {
            if(pr[i] > pr[j]) {
                temp = pr[i]; pr[i] = pr[j]; pr[j] = temp;
                temp = bt[i]; bt[i] = bt[j]; bt[j] = temp;
                temp = p[i]; p[i] = p[j]; p[j] = temp;
            }
        }
    }
    
    wt[0] = 0;
    for(i = 1; i < n; i++)
        wt[i] = wt[i - 1] + bt[i - 1];
        
    for(i = 0; i < n; i++)
        tat[i] = wt[i] + bt[i];
        
    printf("\nProcess\tBT\tPR\tWT\tTAT\n");
    for(i = 0; i < n; i++)
        printf("P%d\t%d\t%d\t%d\t%d\n", p[i], bt[i], pr[i], wt[i], tat[i]);
        
    return 0;
}
```

### 4. Round Robin Scheduling
```c
#include <stdio.h>

int main() {
    int bt[20], rem[20], wt[20], tat[20];
    int n, tq, i, time = 0, done;
    
    printf("Enter number of processes: ");
    scanf("%d", &n);
    
    for(i = 0; i < n; i++) {
        printf("Burst time for P%d: ", i + 1);
        scanf("%d", &bt[i]);
        rem[i] = bt[i];
    }
    
    printf("Enter Time Quantum: ");
    scanf("%d", &tq);
    
    do {
        done = 1;
        for(i = 0; i < n; i++) {
            if(rem[i] > 0) {
                done = 0;
                if(rem[i] > tq) {
                    time += tq;
                    rem[i] -= tq;
                } else {
                    time += rem[i];
                    wt[i] = time - bt[i];
                    rem[i] = 0;
                }
            }
        }
    } while(!done);
    
    for(i = 0; i < n; i++)
        tat[i] = bt[i] + wt[i];
        
    printf("\nProcess\tBT\tWT\tTAT\n");
    for(i = 0; i < n; i++)
        printf("P%d\t%d\t%d\t%d\n", i + 1, bt[i], wt[i], tat[i]);
        
    return 0;
}
```

---

## 📥 Sample Input & Output

**Sample Input Details:**
```text
Number of Processes: 4

Burst Time:
P1 = 5
P2 = 3
P3 = 8
P4 = 6

Priority (for Priority Scheduling):
P1 = 2
P2 = 1
P3 = 4
P4 = 3

Time Quantum (for Round Robin) = 2
```

**1. Sample Output (FCFS):**
```text
Process	BT	WT	TAT
P1	5	0	5
P2	3	5	8
P3	8	8	16
P4	6	16	22
```

**2. Sample Output (SJF):**
```text
Process	BT	WT	TAT
P2	3	0	3
P1	5	3	8
P4	6	8	14
P3	8	14	22
```

**3. Sample Output (Priority Scheduling):**
```text
Process	BT	PR	WT	TAT
P2	3	1	0	3
P1	5	2	3	8
P4	6	3	8	14
P3	8	4	14	22
```

**4. Sample Output (Round Robin):**
```text
Process	BT	WT	TAT
P1	5	11	16
P2	3	8	11
P3	8	14	22
P4	6	14	20
```

---

## ✅ Result
Thus, the CPU Scheduling Algorithms (FCFS, SJF, Priority Scheduling, and Round Robin) were successfully implemented using C programming. The program calculated waiting time and turnaround time for each process and demonstrated how different scheduling strategies affect CPU utilization and process execution order.
