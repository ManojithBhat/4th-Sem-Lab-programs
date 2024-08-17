# Topological sorting using DFS

### code 

``` c
#include <stdio.h>
#include <stdlib.h>
#define MAX 100
int stack[MAX];
int top = -1;

void push(int v) {
    stack[++top] = v;
}

int pop() {
    return stack[top--];
}

int dfs(int node, int visited[], int recStack[], int adj[MAX][MAX], int V) {
    visited[node] = 1;
    recStack[node] = 1; // Mark the current node as being part of the recursion stack

    for (int i = 0; i < V; i++) {
        if (adj[node][i] == 1) {
            if (!visited[i]) {
                if (dfs(i, visited, recStack, adj, V)) {
                    return 1; 
                }
            }
            // If the adjacent vertex is already in the recursion stack, cycle is detected
            else if (recStack[i]) {
                return 1; // Cycle detected
            }
        }
    }

    recStack[node] = 0; // Remove the vertex from the recursion stack after finishing DFS
    push(node); // Push the vertex to the stack after all its neighbors are visited
    return 0;
}


int topologicalSort(int adj[MAX][MAX], int V) {
    int visited[MAX] = {0}; // Array to track visited vertices
    int recStack[MAX] = {0}; // Array to track vertices in the recursion stack

    for (int i = 0; i < V; i++) {
        if (!visited[i]) {
            if (dfs(i, visited, recStack, adj, V)) {
                return 0; // Cycle detected, no topological sort possible
            }
        }
    }

    // If no cycle is detected, print the topological order by popping from the stack
    printf("Topological Sorting: ");
    while (top != -1) {
        printf("%d ", pop());
    }
    printf("\n");
    return 1;
}

int main() {
    int V, E, src, dest;
    int adj[MAX][MAX] = {0}; // Adjacency matrix initialization

    printf("Topological sorting for DIRECTED ACYCLIC GRAPH using DFS method\n");
    printf("Enter the number of vertices: ");
    scanf("%d", &V);
    printf("Enter the number of edges: ");
    scanf("%d", &E);

    int a[E][2]; 

    printf("Enter %d pairs of edges (source -> destination): \n", E);
    for (int i = 0; i < E; i++) {
        scanf("%d %d", &a[i][0], &a[i][1]);

        // Check if the entered edge is valid (no repeated edges, no invalid vertex references)
        for (int j = 0; j < i; j++) {
            if ((a[i][0] == a[j][0]) && (a[i][1] == a[j][1])) {
                printf("WRONG INPUT! Cannot enter repeated edges, try again...\n");
                exit(0);
            }
        }
        if ((a[i][0] < 0 || a[i][0] >= V) || (a[i][1] < 0 || a[i][1] >= V)) {
            printf("WRONG INPUT! Edges having invalid vertex reference...\n");
            exit(0);
        }

        adj[a[i][0]][a[i][1]] = 1; // Fill adjacency matrix
    }

    // Output the vertices and edges
    printf("Vertices: ");
    for (int i = 0; i < V; i++) {
        printf("%d  ", i);
    }
    printf("\nEdges:\n");
    for (int i = 0; i < E; i++) {
        printf("%d -> %d\n", a[i][0], a[i][1]);
    }

    // Perform topological sorting
    if (!topologicalSort(adj, V)) {
        printf("No Topological Order exists (Graph contains a cycle)\n");
    }

    return 0;
}


```

### Reason why this works for detecting cycle 
* Cycle detection in a directed graph during DFS for topological sorting works by tracking the vertices currently being processed in the recursion stack. 
* As we perform DFS, if we encounter a vertex that is already in the recursion stack, it indicates a cycle, since a back edge to a vertex in the same DFS path forms a loop.
* This condition implies that the graph contains a cycle, making topological sorting impossible because topological order can only be achieved in Directed Acyclic Graphs (DAGs). 
* Thus, detecting such revisits helps identify cycles in the graph.

### output 
``` bash
Topological sorting for DIRECTED ACYCLIC GRAPH using DFS method
Enter the number of vertices: 6
Enter the number of edges: 6
Enter 6 pairs of edges (source -> destination): 
5 1
5 1
WRONG INPUT! Cannot enter repeated edges, try again...

```

``` bash
Topological sorting for DIRECTED ACYCLIC GRAPH using DFS method
Enter the number of vertices: 6
Enter the number of edges: 6
Enter 6 pairs of edges (source -> destination): 
5 2
5 0
4 0
4 1
2 3
3 1
Vertices: 0  1  2  3  4  5  
Edges:
5 -> 2
5 -> 0
4 -> 0
4 -> 1
2 -> 3
3 -> 1
Topological Sorting: 5 4 2 3 1 0 

```
