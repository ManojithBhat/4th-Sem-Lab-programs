# Prims Algorithm

```c
#include <stdio.h>
int cost[10][10], n;
void prim()
{
    int vt[10] = {0};
    int a = 0, b = 0, min, mincost = 0, ne = 0;
    // start from the first vertex
    vt[0] = 1;
    while (ne < n - 1)
    {
        // Find the nearest neighbour
        min = 999;
        for (int i = 0; i < n; i++)
        {
            if (vt[i] == 1)
                for (int j = 0; j < n; j++)
                    if (cost[i][j] < min && vt[j] == 0)
                    {
                        min = cost[i][j];
                        a = i;
                        b = j;
                    }
        }
        // Include nearest neighbour 'b' into MST
        printf("Edge from vertex %d to vertex %d and the cost %d\n", a, b, min);
        vt[b] = 1;
        ne++;
        mincost += min;
        cost[a][b] = cost[b][a] = 999;
    }
    printf("minimum spanning tree cost is %d", mincost);
}
void main()
{
    printf("Enter the no. of vertices: ");
    scanf("%d", &n);
    printf("Enter the cost matrix\n");
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            scanf("%d", &cost[i][j]);
    prim();
}

```

