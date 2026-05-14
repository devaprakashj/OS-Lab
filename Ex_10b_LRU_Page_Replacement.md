# Exercise 10b: Implement Page Replacement Algorithms: LRU

## 🎯 Aim
To implement the LRU (Least Recently Used) page replacement algorithm in C using timestamps to evict the least recently used page on a page fault.

## 📝 Algorithm
1. Initialize a `time[]` array to act as recency counters.
2. **On Hit:** If a page is already in the frames, update its time counter: `time[j] = counter++`.
3. **On Miss (Page Fault):** 
   - Fill an empty frame if one is available.
   - If all frames are full, find the frame with the minimum time counter using the `findLRU()` function.
   - Replace the page in that frame and update its counter.
4. Print the frames after every step to visualize the process.
5. Print the total number of page faults at the end.

**Execution Steps:**
1. Create a C file: `gedit lru.c` (or `vim lru.c`).
2. Paste the C code below and save it.
3. Compile the code: `gcc lru.c -o lru`
4. Run the code: `./lru`

---

## 💻 Implementation Code (C Program)

```c
#include <stdio.h>

int findLRU(int time[], int n) {
    int i, minimum = time[0], pos = 0;
    for (i = 1; i < n; ++i) {
        if (time[i] < minimum) {
            minimum = time[i];
            pos = i;
        }
    }
    return pos;
}

int main() {
    int no_of_frames, no_of_pages, frames[10], pages[30];
    int counter = 0, time[10], flag1, flag2, i, j, pos, faults = 0;
    
    printf("Enter number of frames: ");
    scanf("%d", &no_of_frames);
    
    printf("Enter number of pages: ");
    scanf("%d", &no_of_pages);
    
    printf("Enter reference string: ");
    for (i = 0; i < no_of_pages; ++i) 
        scanf("%d", &pages[i]);
        
    for (i = 0; i < no_of_frames; ++i) 
        frames[i] = -1;
        
    for (i = 0; i < no_of_pages; ++i) {
        flag1 = flag2 = 0;
        
        for (j = 0; j < no_of_frames; ++j) {
            if (frames[j] == pages[i]) {
                counter++;
                time[j] = counter;
                flag1 = flag2 = 1;
                break;
            }
        }
        
        if (flag1 == 0) {
            for (j = 0; j < no_of_frames; ++j) {
                if (frames[j] == -1) {
                    counter++;
                    faults++;
                    frames[j] = pages[i];
                    time[j] = counter;
                    flag2 = 1;
                    break;
                }
            }
        }
        
        if (flag2 == 0) {
            pos = findLRU(time, no_of_frames);
            counter++;
            faults++;
            frames[pos] = pages[i];
            time[pos] = counter;
        }
        
        printf("\n");
        for (j = 0; j < no_of_frames; ++j) 
            printf("%d\t", frames[j]);
    }
    
    printf("\n\nTotal Page Faults = %d\n", faults);
    return 0;
}
```

---

## 📥 Sample Input & Output

**Sample Input Details:**
```text
Enter number of frames: 3
Enter number of pages: 6
Enter reference string: 5 7 5 6 7 3
```

**Sample Output (Step-by-step Frame Allocation):**
```text
5	-1	-1	
5	7	-1	
5	7	-1	
5	7	6	
5	7	6	
3	7	6	

Total Page Faults = 4
```

---

## ✅ Result
The LRU page replacement algorithm successfully achieves `4` page faults for the given reference string, demonstrating its effectiveness by tracking recency and outperforming simple FIFO strategies.
