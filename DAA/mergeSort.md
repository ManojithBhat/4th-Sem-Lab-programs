## 1. Merge Sort

### Code 

```c
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

#define N 32000


int merge(int arr[], int low, int mid, int high) {
    
    int count = 0;         
    
    int left = low;
    int right = mid + 1;
    
    int temp[high - low + 1];
    int k = 0;

    while (left <= mid && right <= high) {
        if (arr[left] <= arr[right]) {
            temp[k++] = arr[left++];
        } else {
            temp[k++] = arr[right++];
        }
        count++;
    }

    while (left <= mid) {
        temp[k++] = arr[left++];
        count++;
    }

    while (right <= high) {
        temp[k++] = arr[right++];
        count++;
    }

    for (int i = low; i <= high; i++) {
        arr[i] = temp[i - low];
    }

    return count;
}

int MergeSort(int arr[], int low, int end) {
    int cnt = 0;
    if (low >= end) return 0;
    int mid = (low + end) / 2;
    cnt += MergeSort(arr, low, mid);
    cnt += MergeSort(arr, mid + 1, end);
    cnt += merge(arr, low, mid, end);
    return cnt;
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
            for (i = 0; i < n; i++) {
                scanf("%d", &a[i]);
            }
            MergeSort(a, 0, n - 1);
            printf("Sorted array is:\n");
            for (i = 0; i < n; i++) {
                printf("%d ", a[i]);
            }
            printf("\n");
            break;

        case 2: {
            int arr[32000], size, i, j, t1, t2, t3;
            float ln;
            printf("\nEnter size of array for complexity calculation of array of its next 5 multiples: ");
            scanf("%d", &size);
            printf("\nSize\tAscending\tcnlog(n)\tDescending\tcnlog(n)\tRandom\t\tcnlog(n)\n");

            for (i = 1; i <= 5; i++, size *= 2) {
                ln = 2 * size * log(size) / log(2);
                for (j = 0; j < size; j++) {
                    arr[j] = j;
                }
                t1 = MergeSort(arr, 0, size - 1);

                for (j = 0; j < size; j++) {
                    arr[j] = size - j;
                }
                t2 = MergeSort(arr, 0, size - 1);
                
                for (j = 0; j < size; j++) {
                    arr[j] = rand() % 32000;
                }
                t3 = MergeSort(arr, 0, size - 1);

                printf("%d\t%d\t\t%.0f\t\t%d\t\t%.0f\t\t%d\t\t%.0f\n", size, t1, ln, t2, ln, t3, ln);
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
3 9 27 38 43 82 
```

## Time complexity Analysis 
**Input:**: 2 16

```bash

Enter choice: 1.Correctness 2.Complexity - Enter size of array for complexity calculation of array of its next 5 multiples: 
Size	Ascending	cnlog(n)	Descending	cnlog(n)	Random	cnlog(n)
16	64		128		64		128		64	128
32	160		320		160		320		160	320
64	384		768		384		768		384	768
128	896		1792	896		1792	896	1792
256	2048	4096	2048	4096	2048 4096
(Considering c as 2 here)

```
