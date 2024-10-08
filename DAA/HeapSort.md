## 1. Merge Sort

### Code 

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>
#define N 32000

int heapify(int a[], int n) {
    int i, j, k, v, flag, count = 0;
    for (i = n / 2; i >= 1; i--) {
        k = i;
        v = a[k];
        flag = 0;
        while (!flag && 2 * k <= n) {
            j = 2 * k;
            if (j < n && a[j] < a[j + 1]) {
                j = j + 1;
            }
            if (v >= a[j]) {
                flag = 1;
            } else {
                a[k] = a[j];
                k = j;
                count++;
            }
        }
        if (k != i) {
            a[k] = v;
            count++;
        }
    }
    return count;
}

int heapSort(int a[], int n) {
    int i, temp, swapCount = 0;
    swapCount += heapify(a, n);
    for (i = n; i >= 2; i--) {
        temp = a[1];
        a[1] = a[i];
        a[i] = temp;
        swapCount++;
        swapCount += heapify(a, i - 1);
    }
    return swapCount;
}

int main() {
    int n, i, ch, a[N];
    
    printf("Enter choice: 1.Correctness 2.Complexity - ");
    scanf("%d", &ch);
    switch(ch) {
        case 1:
            printf("Enter the size of array: ");
            scanf("%d", &n);
            printf("Enter %d array elements -\n", n);
            for (i = 1; i <= n; i++) {
                scanf("%d", &a[i]);
            }
            int swaps = heapSort(a, n);
            printf("Sorted array is:\n");
            for (i = 1; i <= n; i++) {
                printf("%d ", a[i]);
            }
            printf("\nNumber of swaps: %d\n", swaps);
            break;
        case 2: {
            int arr[N], size, i, j, t1, t2, t3;
            double ln;
            printf("\nEnter initial size of array for complexity calculation: ");
            scanf("%d", &size);
            printf("\nSize\tAscending\tcnlog(n)\tDescending\tcnlog(n)\tRandom\t\tcnlog(n)\n");
            for (i = 1; i <= 5; i++) {
                if (size > N) break;  // Prevent array overflow
                ln = 2 * size * log2((double)size);
                
                // Ascending order
                for (j = 1; j <= size; j++) arr[j] = j;
                t1 = heapSort(arr, size);
                
                // Descending order
                for (j = 1; j <= size; j++) arr[j] = size - j + 1;
                t2 = heapSort(arr, size);
                
                // Random order
                for (j = 1; j <= size; j++) arr[j] = rand() % N;
                t3 = heapSort(arr, size);
                
                printf("%d\t%d\t\t%.0f\t\t%d\t\t%.0f\t\t%d\t\t%.0f\n", size, t1, ln, t2, ln, t3, ln);
                
                size *= 2;  // Double the size for next iteration
            }
            printf("(Considering c as 2 here)\n");
            break;
        }
        default:
            exit(0);
    }
    return 0;
}

```

### How to run ?
1. Save the file as mergeSort.c
2. run the command gcc mergeSort.c -lm
3. run ./a.out
4. Enter the input 

### Output 
```bash
Enter choice: 1.Correctness 2.Complexity - Enter the size of array: Enter 6 array elements -
Sorted array is:
1 7 9 11 23 45 
Number of swaps: 18
```

## Time complexity Analysis 
**Input:**: 2 16

```bash

Enter choice: 1.Correctness 2.Complexity - 
Enter initial size of array for complexity calculation: 
Size	Ascending	cnlog(n)	Descending	cnlog(n)	Random		cnlog(n)
16	80		128		55		128		74		128
32	192		320		142		320		174		320
64	456		768		350		768		416		768
128	1040		1792		828		1792		962		1792
256	2354		4096		1896		4096		2167		4096
(Considering c as 2 here)

```
