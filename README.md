# Distance-vector-routing-protocol-and-link-state-protocol
#include <stdio.h>
#include <limits.h>

#define MAX_NODES 10

int graph[MAX_NODES][MAX_NODES];
int distanceVector[MAX_NODES][MAX_NODES];
int numNodes;

void initialize() {
    for (int i = 0; i < MAX_NODES; i++) {
        for (int j = 0; j < MAX_NODES; j++) {
            if (i == j) {
                graph[i][j] = 0;
            } else {
                graph[i][j] = INT_MAX;
            }
            distanceVector[i][j] = graph[i][j];
        }
    }
}

void updateDistanceVector() {
    for (int i = 0; i < numNodes; i++) {
        for (int j = 0; j < numNodes; j++) {
            for (int k = 0; k < numNodes; k++) {
                if (distanceVector[i][k] != INT_MAX && distanceVector[k][j] != INT_MAX) {
                    int newDistance = distanceVector[i][k] + distanceVector[k][j];
                    if (newDistance < distanceVector[i][j]) {
                        distanceVector[i][j] = newDistance;
                    }
                }
            }
        }
    }
}

void printDistanceVector() {
    printf("\nDistance Vector Table:\n");
    for (int i = 0; i < numNodes; i++) {
        for (int j = 0; j < numNodes; j++) {
            if (distanceVector[i][j] == INT_MAX) {
                printf("INF\t");
            } else {
                printf("%d\t", distanceVector[i][j]);
            }
        }
        printf("\n");
    }
}

int main() {
    printf("Enter the number of nodes: ");
    scanf("%d", &numNodes);

    printf("Enter the adjacency matrix (INF for infinity):\n");
    for (int i = 0; i < numNodes; i++) {
        for (int j = 0; j < numNodes; j++) {
            scanf("%d", &graph[i][j]);
        }
    }

    initialize();

    printf("\nInitial Graph:\n");
    printDistanceVector();

    updateDistanceVector();

    printDistanceVector();

    return 0;
}









