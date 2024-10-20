
# EXP_6

## Dijkstra’s Algorithm

### Core Algorithm

1. **Initialization**: Set the initial distances from the starting node to all other nodes as infinite, except for the starting node itself, which is set to 0. Create a priority queue and add the starting node.

2. **Processing Nodes**:
   - While the priority queue is not empty:
     - Extract the node with the smallest distance from the queue.
     - For each neighboring node, calculate the distance through the current node.
     - If this new distance is smaller than the known distance, update it and add the neighbor to the priority queue.

3. **Completion**: The algorithm ends when all nodes have been processed, resulting in the shortest paths from the starting node to all other nodes.

### Predefined Version

**CODE**

```python
import heapq

def dijkstra(graph, start):
    # Initialize distances and priority queue
    distances = {node: float('inf') for node in graph}
    distances[start] = 0
    priority_queue = [(0, start)]

    while priority_queue:
        current_distance, current_node = heapq.heappop(priority_queue)

        # Process neighbors
        for neighbor, weight in graph[current_node].items():
            distance = current_distance + weight
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(priority_queue, (distance, neighbor))

    return distances

# Example usage
if __name__ == "__main__":
    graph = {
        'A': {'B': 1, 'C': 4},
        'B': {'A': 1, 'C': 2, 'D': 5},
        'C': {'A': 4, 'B': 2, 'D': 1},
        'D': {'B': 5, 'C': 1}
    }

    start_node = 'A'
    shortest_paths = dijkstra(graph, start_node)

    # Improved output formatting
    print(f"Shortest paths from node '{start_node}':")
    for node, distance in shortest_paths.items():
        if distance < float('inf'):
            print(f"  - Distance to '{node}': {distance}")
        else:
            print(f"  - Distance to '{node}': Unreachable")

```

## User-Defined Dijkstra's Algorithm

**CODE**

```
import heapq

def dijkstra(graph, start):
    distances = {node: float('inf') for node in graph}
    distances[start] = 0
    priority_queue = [(0, start)]

    while priority_queue:
        current_distance, current_node = heapq.heappop(priority_queue)

        # Process neighbors
        for neighbor, weight in graph[current_node].items():
            distance = current_distance + weight
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                heapq.heappush(priority_queue, (distance, neighbor))

    return distances

def input_graph():
    graph = {}
    print("Enter the graph edges in the format 'A B 1' (Node1 Node2 Weight). Type 'done' to finish:")
    
    while True:
        edge = input("Edge: ")
        if edge.lower() == 'done':
            break
        try:
            node1, node2, weight = edge.split()
            weight = int(weight)
            if node1 not in graph:
                graph[node1] = {}
            if node2 not in graph:
                graph[node2] = {}
            graph[node1][node2] = weight
            graph[node2][node1] = weight  # Assuming undirected graph
        except ValueError:
            print("Invalid input. Please enter in the format 'Node1 Node2 Weight'.")
    
    return graph

if __name__ == "__main__":
    # Get user-defined graph
    graph = input_graph()

    # Get the starting node from the user
    start_node = input("Enter the starting node: ")

    # Check if the starting node exists in the graph
    if start_node not in graph:
        print(f"Node '{start_node}' is not in the graph.")
    else:
        shortest_paths = dijkstra(graph, start_node)

        # Improved output formatting
        print(f"\nShortest paths from node '{start_node}':")
        for node, distance in shortest_paths.items():
            if distance < float('inf'):
                print(f"  - Distance to '{node}': {distance}")
            else:
                print(f"  - Distance to '{node}': Unreachable")

```

### Output Example

```
Enter the graph edges in the format 'A B 1' (Node1 Node2 Weight). Type 'done' to finish:
Edge: A B 1
Edge: A C 4
Edge: B C 2
Edge: B D 5
Edge: C D 1
Edge: done
Enter the starting node: A

Shortest paths from node 'A':
  - Distance to 'A': 0
  - Distance to 'B': 1
  - Distance to 'C': 3
  - Distance to 'D': 4

=== Code Execution Successful ===
```
## Code in C
```
#include <stdio.h>
#include <stdbool.h>
#include <limits.h>

#define N 9

// Function to find the vertex with the minimum distance value
int minDist(int dist[N], bool sptSet[N]){
    int cur = INT_MAX, minIdx;

    for (int i = 0; i < N; i++){
        if (!sptSet[i] && dist[i] <= cur){
            cur = dist[i];
            minIdx = i;
        }
    }
    return minIdx;
}

// Function to print the solution
void printSolution(int dist[]){
    printf("Vertex \t\t Distance from Source\n");
    for (int i = 0; i < N; i++)
        printf("%d \t\t\t\t %d\n", i, dist[i]);
}

// Dijkstra's algorithm implementation
void dijkstra(int graph[N][N], int src){
    int dist[N];   // Output array. dist[i] will hold the shortest distance from src to i
    bool sptSet[N]; // sptSet[i] will be true if vertex i is included in the shortest path tree

    // Initialize all distances as INFINITE and sptSet[] as false
    for (int i = 0; i < N; i++) {
        dist[i] = INT_MAX;
        sptSet[i] = false;
    }

    // Distance of source vertex from itself is always 0
    dist[src] = 0;

    // Find shortest path for all vertices
    for (int count = 0; count < N - 1; count++) {
        // Pick the minimum distance vertex from the set of vertices not yet processed
        int u = minDist(dist, sptSet);

        // Mark the picked vertex as processed
        sptSet[u] = true;

        // Update dist[] value of the adjacent vertices of the picked vertex
        for (int v = 0; v < N; v++) {
            // Update dist[v] only if:
            // - It's not in the sptSet
            // - There's an edge from u to v
            // - The total weight of path from src to v through u is smaller than the current value of dist[v]
            if (!sptSet[v] && graph[u][v] && dist[u] != INT_MAX && dist[u] + graph[u][v] < dist[v]) {
                dist[v] = dist[u] + graph[u][v];
            }
        }
    }

    // Print the constructed distance array
    printSolution(dist);
}

int main(){
    // Example graph (can be modified as needed)
    int graph[N][N] = { { 0, 4, 0, 0, 0, 0, 0, 8, 0 },
                        { 4, 0, 8, 0, 0, 0, 0, 11, 0 },
                        { 0, 8, 0, 7, 0, 4, 0, 0, 2 },
                        { 0, 0, 7, 0, 9, 14, 0, 0, 0 },
                        { 0, 0, 0, 9, 0, 10, 0, 0, 0 },
                        { 0, 0, 4, 14, 10, 0, 2, 0, 0 },
                        { 0, 0, 0, 0, 0, 2, 0, 1, 6 },
                        { 8, 11, 0, 0, 0, 0, 1, 0, 7 },
                        { 0, 0, 2, 0, 0, 0, 6, 7, 0 } };

    dijkstra(graph, 0); // Starting from vertex 0

    return 0;
}
```

## Distance Vector Routing Algorithm

### Algorithm

1. **Initialization**: Each router initializes its distance table. The distance to itself is 0, and the distance to all other routers is set to infinity (or a very large number).

2. **Exchange Information**: Each router sends its distance table to its immediate neighbors.

3. **Update Distances**:
   - When a router receives a distance table from a neighbor, it updates its own table using the Bellman-Ford equation:
     \[
     	ext{new\_distance}(destination) = \min(	ext{old\_distance}(destination), 	ext{distance\_to\_neighbor} + 	ext{cost\_to\_neighbor})
     \]
   - If the distance to a destination changes, the router notifies its neighbors of the update.

4. **Repeat**: Steps 2 and 3 are repeated until no more updates occur, indicating that all routers have converged on the shortest paths.

### CODE

```python
class Router:
    def __init__(self, name):
        self.name = name
        self.distance_table = {}
        self.neighbors = {}

    def add_neighbor(self, neighbor, cost):
        self.neighbors[neighbor] = cost
        self.distance_table[neighbor] = cost
        self.distance_table[self.name] = 0  # Distance to itself is 0

    def update_distance_table(self, neighbor_table):
        for destination, distance in neighbor_table.items():
            new_distance = self.distance_table[self.name] + self.neighbors[neighbor] + distance
            if destination not in self.distance_table or new_distance < self.distance_table[destination]:
                self.distance_table[destination] = new_distance
                # Notify neighbors about the update (in real implementation)

# Example usage
if __name__ == "__main__":
    # Create routers
    router_a = Router("A")
    router_b = Router("B")
    router_c = Router("C")

    # Define neighbors and their costs
    router_a.add_neighbor("B", 1)
    router_a.add_neighbor("C", 4)
    router_b.add_neighbor("A", 1)
    router_b.add_neighbor("C", 2)
    router_c.add_neighbor("B", 2)

    # Example of updating distance tables
    router_a.update_distance_table(router_b.distance_table)
    router_b.update_distance_table(router_c.distance_table)

    # Print distance tables
    print(f"Distance table for Router A: {router_a.distance_table}")
    print(f"Distance table for Router B: {router_b.distance_table}")
    print(f"Distance table for Router C: {router_c.distance_table}")
```
## User Define Distance Vector Routing Algorithm 
```
class Router:
    def __init__(self, name):
        self.name = name
        self.distance_table = {}
        self.neighbors = {}

    def add_neighbor(self, neighbor, cost):
        self.neighbors[neighbor] = cost
        self.distance_table[neighbor] = cost
        self.distance_table[self.name] = 0  # Distance to itself is 0

    def update_distance_table(self, neighbor_table):
        for destination, distance in neighbor_table.items():
            # Calculate new distance
            new_distance = self.distance_table[self.name] + self.neighbors[destination] + distance
            # Update distance if the new distance is shorter
            if destination not in self.distance_table or new_distance < self.distance_table[destination]:
                self.distance_table[destination] = new_distance
                # Notify neighbors about the update (in real implementation)

def input_graph():
    routers = {}
    print("Enter the graph edges in the format 'A B 1' (Node1 Node2 Weight). Type 'done' to finish:")
    
    while True:
        edge = input("Edge: ")
        if edge.lower() == 'done':
            break
        try:
            node1, node2, weight = edge.split()
            weight = int(weight)
            if node1 not in routers:
                routers[node1] = Router(node1)
            if node2 not in routers:
                routers[node2] = Router(node2)
            routers[node1].add_neighbor(node2, weight)
            routers[node2].add_neighbor(node1, weight)  # Assuming undirected graph
        except ValueError:
            print("Invalid input. Please enter in the format 'Node1 Node2 Weight'.")

    return routers

if __name__ == "__main__":
    # Get user-defined graph
    routers = input_graph()

    # Simulate distance vector updates
    for router in routers.values():
        for neighbor in router.neighbors.keys():
            router.update_distance_table(routers[neighbor].distance_table)

    # Print distance tables
    for router in routers.values():
        print(f"Distance table for Router {router.name}: {router.distance_table}")

```
## Output
```
Enter the graph edges in the format 'A B 1' (Node1 Node2 Weight). Type 'done' to finish:
Edge: A B 1
Edge: A C 4
Edge: B C 2
Edge: B D 5
Edge: C D 1
Edge: done

```
### Key Differences Between the Algorithms

- **Dijkstra's Algorithm** focuses on finding the shortest path from a single source to all other nodes, using a priority queue to explore the nearest nodes first.
- **Distance Vector Routing** focuses on maintaining and updating distance tables among all routers in the network, using information shared from neighbors.

Both algorithms serve important roles in network routing but operate on different principles and methods of communication.
