# Exercise 10a: Implement Page Replacement Algorithms: FIFO

## 🎯 Aim
To implement the FIFO (First-In, First-Out) page replacement algorithm in C to simulate evicting the oldest page on a page fault.

## 📝 Algorithm
1. Initialize all page frames to `-1` (indicating they are empty).
2. For each page in the reference string:
   - Check if the page is already in the frames (**Hit**).
   - If not found, a **Page Fault** occurs.
3. Replace the page at the next available position in a circular queue manner using the formula:  
   `j = (j + 1) % no_of_frames`
4. Increment the page fault count.
5. Print the total number of page faults at the end.

**Execution Steps:**
1. Create a C file: `gedit fifo.c` (or `vim fifo.c`).
2. Paste the C code below and save it.
3. Compile the code: `gcc fifo.c -o fifo`
4. Run the code: `./fifo`

---

## 💻 Implementation Code (C Program)

```c
#include <stdio.h>
#include <stdlib.h>

int pagefault(int a[], int frame[], int n, int no) {
    int i, j = 0, count = 0, k;
    
    for (i = 0; i < no; i++) 
        frame[i] = -1;
        
    for (i = 0; i < n; i++) {
        int avail = 0;
        for (k = 0; k < no; k++) {
            if (frame[k] == a[i]) 
                avail = 1;
        }
        if (avail == 0) {
            frame[j] = a[i];
            j = (j + 1) % no;
            count++;
        }
    }
    return count;
}

int main() {
    int n, no, fault, i;
    int *a, *frame;
    
    printf("ENTER THE NUMBER OF PAGES: ");
    scanf("%d", &n);
    
    a = (int*)malloc(n * sizeof(int));
    
    printf("ENTER THE PAGE NUMBER: ");
    for (i = 0; i < n; i++) 
        scanf("%d", &a[i]);
        
    printf("ENTER THE NUMBER OF FRAMES: ");
    scanf("%d", &no);
    
    frame = (int*)malloc(no * sizeof(int));
    fault = pagefault(a, frame, n, no);
    
    printf("Page Faults: %d\n", fault);
    
    return 0;
}
```

---

## 📥 Sample Input & Output

**Sample Input Details:**
```text
ENTER THE NUMBER OF PAGES: 7
ENTER THE PAGE NUMBER: 1 4 0 4 5 3 7
ENTER THE NUMBER OF FRAMES: 3
```

**Sample Output:**
```text
Page Faults: 6
```

---

## ✅ Result
The FIFO page replacement algorithm correctly computes `6` page faults for the example, replacing the oldest pages first, demonstrating the First-In, First-Out methodology in memory management.
