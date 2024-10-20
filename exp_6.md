
# EXP_6

## Dijkstra’s Algorithm

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

```python
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

