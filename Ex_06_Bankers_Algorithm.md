# Exercise 6: Implementation of Banker’s Algorithm for Deadlock Avoidance

## 🎯 Aim
To write and execute a C program to implement the Banker's Algorithm that takes Allocation, Maximum, and Available matrices as input, computes the Need matrix, and determines whether the system is in a safe state. If the system is safe, the program also prints the safe sequence of process execution.

## 📝 Procedure

**Common Setup Step:**
1. Open the Linux terminal.
2. It's recommended to do this in a separate folder: `mkdir Ex_06` and then `cd Ex_06`.

**Algorithm Steps:**
1. Start the program and read the number of processes (`p`) and number of resources (`r`).
2. Input the **Allocation matrix**, which represents the resources currently allocated to each process.
3. Input the **Maximum matrix**, which represents the maximum resources each process may require.
4. Input the **Available resources** vector.
5. Compute the **Need matrix** using the formula:  
   `Need[i][j] = Max[i][j] − Allocation[i][j]`
6. Initialize:
   - `Work = Available`
   - `Finish[i] = false` for all processes.
7. Find a process such that:
   - `Finish[i] = false`
   - `Need[i] ≤ Work`
8. If such a process is found:
   - Add its allocation to Work.
   - Mark `Finish[i] = true`.
   - Add the process to the safe sequence.
9. Repeat until all processes are completed or no process satisfies the condition.
10. If all processes finish successfully, the system is in a safe state; otherwise it is unsafe.

**Execution Steps:**
1. Create a C file: `gedit bankers.c` (or `vim bankers.c`).
2. Paste the C code below and save it.
3. Compile the code: `gcc bankers.c -o bankers`
4. Run the code: `./bankers`

---

## 💻 Implementation Code (C Program)

```c
#include <stdio.h>

int main() {
    int p, r, i, j, count = 0;
    
    printf("Enter number of processes and resources: ");
    scanf("%d %d", &p, &r);
    
    int allocation[10][10], max[10][10], need[10][10];
    int available[10], safe[10], done[10];
    
    printf("Enter allocation matrix:\n");
    for (i = 0; i < p; i++)
        for (j = 0; j < r; j++)
            scanf("%d", &allocation[i][j]);
            
    printf("Enter max matrix:\n");
    for (i = 0; i < p; i++)
        for (j = 0; j < r; j++)
            scanf("%d", &max[i][j]);
            
    printf("Enter available resources:\n");
    for (i = 0; i < r; i++)
        scanf("%d", &available[i]);
        
    printf("\nNeed Matrix:\n");
    for (i = 0; i < p; i++) {
        for (j = 0; j < r; j++) {
            need[i][j] = max[i][j] - allocation[i][j];
            printf("%d ", need[i][j]);
        }
        printf("\n");
    }
    
    for (i = 0; i < p; i++)
        done[i] = 0;
        
    while (count < p) {
        int found = 0;
        for (i = 0; i < p; i++) {
            if (done[i] == 0) {
                int flag = 1;
                for (j = 0; j < r; j++) {
                    if (need[i][j] > available[j]) {
                        flag = 0;
                        break;
                    }
                }
                if (flag) {
                    safe[count] = i;
                    done[i] = 1;
                    for (j = 0; j < r; j++)
                        available[j] += allocation[i][j];
                    count++;
                    found = 1;
                }
            }
        }
        if (!found) {
            printf("\nSystem is in Unsafe State\n");
            return 0;
        }
    }
    
    printf("\nSafe Sequence: ");
    for (i = 0; i < p; i++)
        printf("P%d ", safe[i]);
    printf("\nSystem is in Safe State\n");
    
    return 0;
}
```

---

## 📥 Sample Input & Output

**Sample Input Details:**
```text
Enter number of processes and resources: 5 3

Enter allocation matrix:
0 1 0
2 0 0
3 0 2
2 1 1
0 0 2

Enter max matrix:
7 5 3
3 2 2
9 0 2
6 2 2
4 3 3

Enter available resources:
3 3 2
```

**Sample Output:**
```text
Need Matrix:
7 4 3 
1 2 2 
6 0 0 
4 1 1 
4 3 1 

Safe Sequence: P1 P3 P4 P0 P2 
System is in Safe State
```

---

## ✅ Result
The Banker’s Algorithm program was successfully implemented and executed. 
The program calculated the Need matrix and determined that the system is in a safe state with the safe execution sequence: `P1 → P3 → P4 → P0 → P2`. 
Thus, the system can allocate resources without leading to deadlock.
