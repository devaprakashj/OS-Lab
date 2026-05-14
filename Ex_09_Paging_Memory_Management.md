# Exercise 9: Implement Paging Technique of Memory Management

## 🎯 Aim
To implement paging memory management in C, allowing input of page tables for multiple processes and translating logical addresses to physical addresses.

## 📚 Theory
This exercise simulates paging in C, where logical addresses map to physical addresses via page tables, dividing memory into fixed-size pages and frames.
Paging eliminates external fragmentation by allocating fixed-size pages to non-contiguous frames. A page table maps logical page numbers to physical frame numbers.

**Formula:**
`Physical Address = (Frame_No * Page_Size) + Offset`

## 📝 Algorithm
1. Input memory size (`ms`), page size (`ps`); compute total pages `nop = ms / ps`.
2. Input number of processes (`np`).
3. For each process, input pages needed (`s[i]`), check if memory is sufficient, then input the page table `fno[i][j]` (frame numbers).
4. Input logical address as (process_no `x`, page_no `y`, offset).
5. Compute physical address `pa = fno[x][y] * ps + offset`. Validate inputs before calculating.

---

## 💻 Implementation Code (C Program)

> **Note:** The code has been adapted for Linux (removed `<conio.h>` and `clrscr()` which are Windows/DOS specific) so it compiles perfectly using `gcc` in Red Hat.

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int ms, ps, nop, np, rempages, i, j, x, y, pa, offset;
    int s[10], fno[10][20];
    
    printf("\nEnter the memory size -- ");
    scanf("%d", &ms);
    
    printf("\nEnter the page size -- ");
    scanf("%d", &ps);
    
    nop = ms / ps;
    printf("\nThe no. of pages available in memory are -- %d \n", nop);
    
    printf("\nEnter number of processes -- ");
    scanf("%d", &np);
    
    rempages = nop;
    
    for (i = 1; i <= np; i++) {
        printf("\nEnter no. of pages required for p[%d]-- ", i);
        scanf("%d", &s[i]);
        
        if (s[i] > rempages) {
            printf("\nMemory is Full\n");
            break;
        }
        
        rempages = rempages - s[i];
        
        printf("Enter pagetable for p[%d] --- ", i);
        for (j = 0; j < s[i]; j++)
            scanf("%d", &fno[i][j]);
    }
    
    printf("\nEnter Logical Address to find Physical Address ");
    printf("\nEnter process no. and pagenumber and offset -- ");
    scanf("%d %d %d", &x, &y, &offset);
    
    if (x > np || y >= s[x] || offset >= ps)
        printf("\nInvalid Process or Page Number or offset\n");
    else {
        pa = fno[x][y] * ps + offset;
        printf("\nThe Physical Address is -- %d\n", pa);
    }
    
    return 0;
}
```

---

## 📥 Sample Input & Output

**Execution & Input Details:**
```text
Enter the memory size -- 1000

Enter the page size -- 100

The no. of pages available in memory are -- 10 

Enter number of processes -- 3

Enter no. of pages required for p[1]-- 4
Enter pagetable for p[1] --- 8 6 9 5

Enter no. of pages required for p[2]-- 5
Enter pagetable for p[2] --- 1 4 5 7 3

Enter no. of pages required for p[3]-- 5

Memory is Full

Enter Logical Address to find Physical Address 
Enter process no. and pagenumber and offset -- 2 3 60
```

**Output:**
```text
The Physical Address is -- 760
```

---

## ✅ Result
The program successfully simulates multi-process paging, allocating pages to frames and computing the physical address `760` from logical (process 2, page 3, offset 60) with a page size of 100.
