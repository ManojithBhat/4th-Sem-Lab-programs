## Floyd's Algorithm
```c
#include<stdio.h>

int min(int a, int b)
{
    return (a < b ? a : b);
}

void floyd(int D[10][10], int n)
{
    for (int k = 0; k < n; k++)
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                D[i][j] = min(D[i][j], D[i][k] + D[k][j]);
}

int main()
{
    int n, cost[10][10];
    printf("\nEnter the number of vertices: ");
    scanf("%d", &n);
    if (n > 10) 
    {
        printf("Maximum allowed vertices is 10.\n");
        return -1;
    }

    printf("\nEnter the cost matrix (use a large number for INF):\n");
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            printf("cost[%d][%d]: ", i, j);
            scanf("%d", &cost[i][j]);
        }
    }

    floyd(cost, n);

    printf("\nAll pair shortest path matrix:\n");
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            printf("%d ", cost[i][j]);
        }
        printf("\n");
    }

    return 0;
}

```
