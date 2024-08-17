# Djikstra Shortest Path Algorithm

### code 
``` cpp
#include <stdio.h>
#define INFINITY 999

void dijk(int cost[10][10], int n, int source, int v[10], int d[10]) {
    int least, i, j, u;
    
    v[source] = 1;

    for (i = 1; i <= n; i++) {
        least = INFINITY;
        // Find the next nearest node u
        for (j = 1; j <= n; j++) {
            if (v[j] == 0 && d[j] < least) {
                least = d[j];
                u = j;
            }
        }
        v[u] = 1;
        
        // Update the distance for remaining nodes
        for (j = 1; j <= n; j++) {
            if (d[j] > d[u] + cost[u][j]) {
                d[j] = d[u] + cost[u][j];
            }
        }
    }
}

int main() {
    int n;  
    int cost[10][10]; 
    int source;  // Source node
    int v[10];  // Visited array
    int d[10];  // Distance array
    int i, j;  // Index variables

    // Read number of nodes
    printf("Enter n: ");
    scanf("%d", &n);

    // Read the cost adjacency matrix of the graph
    printf("Enter Cost matrix:\n");
    for (i = 1; i <= n; i++) {
        for (j = 1; j <= n; j++) {
            scanf("%d", &cost[i][j]);
        }
    }

    // Read source node
    printf("Enter source: ");
    scanf("%d", &source);

    // Initialize d[] to distance from source to each node
    // Initialize v[] to 0, indicating none of the nodes are visited
    for (i = 1; i <= n; i++) {
        d[i] = cost[source][i];
        v[i] = 0;
    }
    d[source] = 0;  // Distance from source to itself is 0

    // Call function to compute shortest distance
    dijk(cost, n, source, v, d);

    // Print shortest distance from source to all other nodes
    printf("Shortest distance from source %d:\n", source);
    for (i = 1; i <= n; i++) {
        printf("%d --> %d = %d\n", source, i, d[i]);
    }

    return 0;
}

```

### Output 

``` bash

Enter n: 4
Enter Cost matrix:
0 10 15 20
10 0 35 25
15 35 0 30
20 25 30 0

Enter source: 1
Shortest distance from source 1:
1 --> 1 = 0
1 --> 2 = 10
1 --> 3 = 15
1 --> 4 = 20

```
