# **Unit 2: Artificial Intelligence Search Techniques**

- **Run Artificial Intelligence Search Techniques(Hands-on).ipynb Notebook in Google Colab:** <a href="https://colab.research.google.com/github/Harshit-Soni78/Intelligent-Computing-Techniques/blob/main/Unit%202%20(Artificial%20Intelligence%20Search%20Techniques)/Artificial%20Intelligence%20Search%20Techniques(Hands-on).ipynb" target="_blank">Click Here 🔗</a>

---

## **1. Introduction to AI Search Techniques**

### **What is Search in AI?**

Search is a fundamental problem-solving technique in Artificial Intelligence. It involves exploring possible solutions to reach a goal state from an initial state efficiently.

### **Types of Search Techniques:**

1. **Uninformed Search (Blind Search):** No additional information is available beyond the problem definition.
   - Breadth-First Search (BFS)
   - Depth-First Search (DFS)
   - Uniform Cost Search
2. **Informed Search (Heuristic Search):** Uses problem-specific knowledge to improve efficiency.
   - Best-First Search
   - A\* Algorithm
   - AO\* Algorithm
3. **Local Search Algorithms:** Used for optimization problems.
   - Hill Climbing
   - Simulated Annealing

---

## **2. Hands-on: Implementing Search Algorithms in Python**

### **Breadth-First Search (BFS)**

```python
from collections import deque

def bfs(graph, start):
    visited = set()
    queue = deque([start])
    while queue:
        node = queue.popleft()
        if node not in visited:
            print(node, end=" ")
            visited.add(node)
            queue.extend(graph[node])

# Graph representation
graph = {
    'A': ['B', 'C'],
    'B': ['D', 'E'],
    'C': ['F'],
    'D': [],
    'E': ['F'],
    'F': []
}

print("BFS Traversal:")
bfs(graph, 'A')
```

**Explanation:** BFS explores nodes level by level, ensuring the shortest path in an unweighted graph.

---

### **Depth-First Search (DFS)**

```python
def dfs(graph, node, visited=None):
    if visited is None:
        visited = set()
    if node not in visited:
        print(node, end=" ")
        visited.add(node)
        for neighbor in graph[node]:
            dfs(graph, neighbor, visited)

print("\nDFS Traversal:")
dfs(graph, 'A')
```

**Explanation:** DFS explores as far as possible along a branch before backtracking.

---

### **Hill Climbing Algorithm (Local Search)**

```python
import random

def hill_climb(problem, max_iterations=100):
    current = problem()
    for _ in range(max_iterations):
        neighbor = problem()
        if neighbor > current:
            current = neighbor
    return current

# Example: Finding maximum of a random function
def sample_problem():
    return random.randint(1, 100)

print("Best Solution Found:", hill_climb(sample_problem))
```

**Explanation:** Hill climbing is an optimization technique that moves towards the highest-value neighboring state.

---

### **A\* Algorithm for Pathfinding**

```python
import heapq

def a_star(graph, start, goal, heuristic):
    open_list = []
    heapq.heappush(open_list, (0, start))
    came_from = {}
    g_score = {node: float('inf') for node in graph}
    g_score[start] = 0
    f_score = {node: float('inf') for node in graph}
    f_score[start] = heuristic[start]

    while open_list:
        _, current = heapq.heappop(open_list)
        if current == goal:
            path = []
            while current in came_from:
                path.append(current)
                current = came_from[current]
            return path[::-1]

        for neighbor, cost in graph[current].items():
            tentative_g_score = g_score[current] + cost
            if tentative_g_score < g_score[neighbor]:
                came_from[neighbor] = current
                g_score[neighbor] = tentative_g_score
                f_score[neighbor] = g_score[neighbor] + heuristic[neighbor]
                heapq.heappush(open_list, (f_score[neighbor], neighbor))
    return None

# Example Graph
graph = {
    'A': {'B': 1, 'C': 4},
    'B': {'A': 1, 'D': 2, 'E': 5},
    'C': {'A': 4, 'F': 3},
    'D': {'B': 2},
    'E': {'B': 5, 'F': 1},
    'F': {'C': 3, 'E': 1}
}

heuristic = {'A': 7, 'B': 6, 'C': 2, 'D': 3, 'E': 1, 'F': 0}

print("A* Path from A to F:", a_star(graph, 'A', 'F', heuristic))
```

**Explanation:** A\* uses heuristics to find the shortest path efficiently.

---

## **3. Discussion Questions**

1. How does informed search improve upon uninformed search?
2. Why does Hill Climbing sometimes get stuck in local optima?
3. What real-world applications use A\* and heuristic-based search?

## Author

**Harshit Soni**  
GitHub: [Harshit-Soni78](https://github.com/Harshit-Soni78)

---
Made with ❤️ by Harshit Soni
