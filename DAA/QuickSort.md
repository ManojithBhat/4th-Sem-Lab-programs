# Quick Sort

### code

```c

#include <stdio.h>
#include <stdlib.h>
#include <math.h>

int N;

int QuickSort(int[], int, int);
int *Partition(int[], int, int);
void swap(int *, int *);


int QuickSort(int arr[N], int left, int right)
{
    if (left>=right || left < 0 || right < 0)
        return 0;

    int s, c1 = 0, c2 = 0, count = 0, *c;

    c = Partition(arr, left, right);
    s = c[0];
    count = c[1];

    c1 = QuickSort(arr, left, s - 1);
    c2 = QuickSort(arr, s + 1, right);

   // free(c); 
    return count + c1 + c2;
}

int *Partition(int arr[N], int left, int right)
{
    int i = left + 1, j = right, count = 0;
    int pivot = arr[left];
    int *c = (int *)malloc(sizeof(int) * 2);

    while (i <= j)
    {
        while (pivot>=arr[i] && i<=right)
        {
            i++;
            count++;
        }
        while (pivot<arr[j])
        {
            j--;
            count++;
        }

        if (i < j)
        {
            swap(&arr[i], &arr[j]);
        }
    }

    swap(&arr[left], &arr[j]);
    c[0] = j; // Return final pivot position
    c[1] = count;

    return c;
}

void swap(int *a, int *b)
{
    int t = *a;
    *a = *b;
    *b = t;
}

int main()
{
    int n, i, ch, x;
    printf("Enter choice: 1.Correctness 2.Complexity - ");
    scanf("%d", &ch);

    switch (ch)
    {
    case 1:
    {
        printf("Enter the size of array: ");
        scanf("%d", &n);
        
        int a[n];
        printf("Enter %d array elements -\n", n);
        for (i = 0; i < n; i++)
            scanf("%d", &a[i]);

        x = QuickSort(a, 0, n - 1);
        printf("Sorted array is:\n");
        for (i = 0; i < n; i++)
            printf("%d ", a[i]);
        printf("\n");
        break;
    }
    case 2:
    {
        int arr[32000], size, i, j, t1, t2, t3;
        float ln;
        printf("Enter size of array for complexity calculation of array of its next 5 multiples: ");
        scanf("%d", &size);
        printf("Size\tAscending\t(n*n)\t\tDescending\t(n*n)\tRandom \t(3nlogn)\n");

        for (i = 1; i <= 5; i++, size *= 2)
        {
            
            ln = 3 * size * log(size) / log(2);
          
            for (j = 0; j < size; j++)
                arr[j] = j;
            t1 = QuickSort(arr, 0, size - 1);


            for (j = 0; j < size; j++)
                arr[j] = size - j;
            t2 = QuickSort(arr, 0, size - 1);


            for (j = 0; j < size; j++)
                arr[j] = rand() % 32000;
            t3 = QuickSort(arr, 0, size - 1);

            printf("%d\t%d\t\t%d\t\t%d\t\t%.d\t%d\t%.0f\n", size, t1, size * size, t2, size * size, t3, ln);
        }
        break;
    }
      default:
      {
        exit(0);
      }
    }

    return 0;
}

```
### Input
```bash
Enter choice: 1.Correctness 2.Complexity -
1
Enter the size of array:
6
Enter 6 array elements -
12 34 1 5 45 10
```

###  Output 
```bash
Sorted array is:
1 5 10 12 34 45 
```

### Time complexity Analysisi
```bash
Size	Ascending	(n*n)		Descending	(n*n)	Random 	(3nlogn)
16	120		256		120		256	72	192
32	496		1024		496		1024	151	480
64	2016		4096		2016		4096	364	1152
128	8128		16384		8128		16384	990	2688
256	32640		65536		32640		65536	1877	6144
```

