# Exercise 7: Implementation of Deadlock Detection Algorithm

## 🎯 Aim
To write and execute a C program to implement the Deadlock Detection Algorithm in the Operating Systems, which detects whether the system is in a deadlock state by analyzing the Allocation matrix, Request matrix, and Available resources.

## 📝 Procedure

**Common Setup Step:**
1. Open the Linux terminal.
2. It's recommended to do this in a separate folder: `mkdir Ex_07` and then `cd Ex_07`.

**Algorithm Steps:**
1. Start the program.
2. Enter the number of processes (`n`) and number of resource types (`m`).
3. Enter the **Allocation matrix**, representing resources currently allocated to each process.
4. Enter the **Request matrix**, representing the resources currently requested by each process.
5. Enter the **Available resource** vector.
6. Initialize:
   - `Work = Available`
   - `Finish[i] = false` for all processes.
7. Find a process `Pi` such that:
   - `Finish[i] = false`
   - `Request[i] ≤ Work`
8. If such a process exists:
   - Add its allocated resources to Work.
   - Mark `Finish[i] = true`.
9. Repeat the above steps until no such process can be found.
10. If any process remains with `Finish[i] = false`, then the system is in a deadlock state.

**Execution Steps:**
1. Create a C file: `gedit deadlock_detection.c` (or `vim deadlock_detection.c`).
2. Paste the C code below and save it.
3. Compile the code: `gcc deadlock_detection.c -o deadlock_detection`
4. Run the code: `./deadlock_detection`

---

## 💻 Implementation Code (C Program)

```c
#include <stdio.h>

int main() {
    int n, m, i, j;
    
    printf("Enter number of processes: ");
    scanf("%d", &n);
    printf("Enter number of resources: ");
    scanf("%d", &m);
    
    int allocation[n][m], request[n][m], available[m];
    int finish[n], work[m];
    
    printf("Enter Allocation Matrix:\n");
    for(i = 0; i < n; i++)
        for(j = 0; j < m; j++)
            scanf("%d", &allocation[i][j]);
            
    printf("Enter Request Matrix:\n");
    for(i = 0; i < n; i++)
        for(j = 0; j < m; j++)
            scanf("%d", &request[i][j]);
            
    printf("Enter Available Resources:\n");
    for(i = 0; i < m; i++) {
        scanf("%d", &available[i]);
        work[i] = available[i];
    }
    
    for(i = 0; i < n; i++)
        finish[i] = 0;
        
    int found;
    do {
        found = 0;
        for(i = 0; i < n; i++) {
            if(!finish[i]) {
                int possible = 1;
                for(j = 0; j < m; j++) {
                    if(request[i][j] > work[j]) {
                        possible = 0;
                        break;
                    }
                }
                if(possible) {
                    for(j = 0; j < m; j++)
                        work[j] += allocation[i][j];
                    finish[i] = 1;
                    found = 1;
                }
            }
        }
    } while(found);
    
    int deadlock = 0;
    for(i = 0; i < n; i++) {
        if(!finish[i]) {
            deadlock = 1;
            printf("Process P%d is in deadlock\n", i);
        }
    }
    
    if(!deadlock)
        printf("No Deadlock Detected\n");
        
    return 0;
}
```

---

## 📥 Sample Input & Output

**Sample Input Details:**
```text
Number of Processes: 3
Number of Resource Types: 2

Allocation Matrix:
1 0
0 1
1 1

Request Matrix:
0 1
1 0
1 0

Available Resources:
1 0
```

**Sample Output:**
```text
No Deadlock Detected
```

**Example of Deadlock Situation (If it happens):**
```text
Process P1 is in deadlock
Process P2 is in deadlock
```

---

## ✅ Result
Thus, the Deadlock Detection Algorithm was successfully implemented using C programming. 
The program analyzes the Allocation, Request, and Available matrices to determine whether the system is in a deadlock state and identifies the processes involved in deadlock.
