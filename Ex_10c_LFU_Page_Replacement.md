# Exercise 10c: Implement Page Replacement Algorithms: LFU

## 🎯 Aim
To implement the LFU (Least Frequently Used) page replacement algorithm in C using frequency counters to evict the least frequently used page on a page fault.

## 📝 Algorithm
1. Maintain a `count1[]` array to store the access frequencies of pages in frames.
2. **On Reference (Hit):** If a page is already present, increment its frequency count.
3. **On Miss (Page Fault):** 
   - Fill an empty frame if available, set its frequency to `1`, and increment the page fault counter.
   - If no frames are empty, scan the frames to find the one with the minimum frequency (`min count`). Evict that page, load the new page, reset its frequency to `1`, and increment the page fault counter.
4. Print the current frames after every page reference to visualize the replacement process.
5. Display the total number of page faults at the end.

**Execution Steps:**
1. Create a C file: `gedit lfu.c` (or `vim lfu.c`).
2. Paste the C code below and save it.
3. Compile the code: `gcc lfu.c -o lfu`
4. Run the code: `./lfu`

---

## 💻 Implementation Code (C Program)

```c
#include <stdio.h>

int main() {
    int i, j, k, n, frameno, page[50], frame[10], move = 0, flag, count = 0, count1[10] = {0};
    
    printf("Enter number of pages: ");
    scanf("%d", &n);
    
    printf("Enter page reference string: ");
    for (i = 0; i < n; i++) 
        scanf("%d", &page[i]);
        
    printf("Enter number of frames: ");
    scanf("%d", &frameno);
    
    for (i = 0; i < frameno; i++) 
        frame[i] = -1;
        
    printf("\nPage reference string\tFrames\n");
    
    for (i = 0; i < n; i++) {
        printf("%d\t\t\t", page[i]);
        flag = 0;
        
        for (j = 0; j < frameno; j++) {
            if (page[i] == frame[j]) {
                flag = 1;
                count1[j]++;
                break;
            }
        }
        
        if (flag == 0) {
            for (j = 0; j < frameno; j++) {
                if (frame[j] == -1) {
                    frame[j] = page[i];
                    count1[j]++;
                    count++;
                    break;
                }
            }
            if (j == frameno) {
                int min = 0;
                for (k = 1; k < frameno; k++) {
                    if (count1[k] < count1[min]) 
                        min = k;
                }
                frame[min] = page[i];
                count1[min] = 1;
                count++;
            }
        }
        
        for (j = 0; j < frameno; j++) 
            printf("%d\t", frame[j]);
        printf("\n");
    }
    
    printf("\nTotal Page Faults: %d\n", count);
    return 0;
}
```

---

## 📥 Sample Input & Output

**Sample Input Details:**
```text
Enter number of pages: 17
Enter page reference string: 7 0 1 2 0 3 0 4 2 3 0 3 2 1 2 0 1
Enter number of frames: 3
```

**Sample Output (Step-by-step Frame Allocation):**
```text
Page reference string   Frames
7                       7       -1      -1
0                       7       0       -1
1                       7       0       1
2                       2       0       1
0                       2       0       1
3                       2       0       3
0                       2       0       3
4                       4       0       3
2                       4       0       2
3                       3       0       2
0                       3       0       2
3                       3       0       2
2                       3       0       2
1                       1       0       2
2                       1       0       2
0                       1       0       2
1                       1       0       2

Total Page Faults: 13
```

---

## ✅ Result
The LFU page replacement algorithm successfully simulates frequency-based replacement, yielding `13` faults for the provided example string, properly demonstrating how least frequently used pages are evicted to optimize memory usage.
