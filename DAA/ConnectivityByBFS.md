## Check the connectivity of Graph by BFS
### code 
``` c
#include <stdio.h>
#include <stdlib.h>

#define MAX 100

int adjMatrix[MAX][MAX], visited[MAX];
int queue[MAX], front = -1, rear = -1;
int n; // Number of vertices

void enqueue(int v) {
    if (rear == MAX - 1) {
        printf("Queue is full\n");
        return;
    }
    if (front == -1) front = 0;
    rear++;
    queue[rear] = v;
}

int dequeue() {
    if (front == -1 || front > rear) {
        printf("Queue is empty\n");
        return -1;
    }
    int v = queue[front];
    front++;
    return v;
}

int isQueueEmpty() {
    return front == -1 || front > rear;
}

void BFS(int start) {
    enqueue(start);
    visited[start] = 1;

    while (!isQueueEmpty()) {
        int currentVertex = dequeue();
        for (int i = 0; i < n; i++) {
            if (adjMatrix[currentVertex][i] == 1 && !visited[i]) {
                enqueue(i);
                visited[i] = 1;
            }
        }
    }
}

int isGraphConnected() {
    // Check connectivity by starting BFS from vertex 0
    BFS(0);

    // If any vertex is not visited, the graph is not connected
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            return 0; // Graph is not connected
        }
    }
    return 1; // Graph is connected
}

int main() {
    printf("Enter the number of vertices: ");
    scanf("%d", &n);

    printf("Enter the adjacency matrix (space separated, 0/1 for each element):\n");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            scanf("%d", &adjMatrix[i][j]);
        }
    }

    // Initialize visited array to 0
    for (int i = 0; i < n; i++) {
        visited[i] = 0;
    }

    if (isGraphConnected()) {
        printf("The graph is connected.\n");
    } else {
        printf("The graph is not connected.\n");
    }

    return 0;
}

```
### input
```bash
Enter the number of vertices: 4
Enter the adjacency matrix (space separated, 0/1 for each element):<br>
0 1 0 0
1 0 0 0
0 0 0 1
0 0 1 0

```

### output 
``` bash
The graph is not connected.
```
