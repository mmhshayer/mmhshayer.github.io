---
author: "Mohammad Mustakim Hassan"
title: "Breadth First Search"
date: "2023-05-06"
description: "Notes on Breadth First Search (BFS)"
tags: ["algorithm", "search", "graph"]
ShowToc: true
---

## Introduction
Breadth First Search (BFS) is a graph traversal algorithm that explores all the vertices in a graph level by level. It starts at the initial vertex (source node) and explores all the neighbor vertices at the current level before moving to the next level.

## Algorithm Steps
- Start at the initial vertex (source node).
- Enqueue the initial vertex.
- Visit the initial vertex and mark it as visited.
- Dequeue the current vertex and enqueue its adjacent unvisited vertices.
- Repeat the process until all vertices are visited.

## Example
Consider the following graph:
```
     A
   / | \
  B  |  C
 / \ | / \
D   E F   G
```
Starting from vertex A, a breadth-first traversal would visit vertices in the order: A -> B -> C -> D -> E -> F -> G.

## JavaScript Implementation
```javascript
class Graph {
    constructor() {
        this.vertices = {};
    }

    addVertex(vertex) {
        if (!this.vertices[vertex]) {
            this.vertices[vertex] = [];
        }
    }

    addEdge(source, destination) {
        this.vertices[source].push(destination);
    }

    breadthFirstSearch(start) {
        const visited = {};
        const traversalOrder = [];
        const queue = [];

        visited[start] = true;
        queue.push(start);

        while (queue.length !== 0) {
            const currentVertex = queue.shift();
            traversalOrder.push(currentVertex);

            this.vertices[currentVertex].forEach((neighbor) => {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.push(neighbor);
                }
            });
        }

        return traversalOrder;
    }
}

// Example usage
const graph = new Graph();
graph.addVertex('A');
graph.addVertex('B');
graph.addVertex('C');
graph.addVertex('D');
graph.addVertex('E');
graph.addVertex('F');
graph.addVertex('G');

graph.addEdge('A', 'B');
graph.addEdge('A', 'C');
graph.addEdge('B', 'D');
graph.addEdge('B', 'E');
graph.addEdge('C', 'F');
graph.addEdge('C', 'G');

const traversalOrder = graph.breadthFirstSearch('A');
console.log('Breadth First Search Traversal Order:', traversalOrder);
// Breadth First Search Traversal Order: [ 'A', 'B', 'C', 'D', 'E', 'F', 'G' ]
```

## Complexity Analysis
The time complexity of Breadth First Search is O(V + E), where V is the number of vertices and E is the number of edges in the graph. 
The space complexity is O(V) due to the queue used in the algorithm.

## Advantage and Disadvantage

### Advantage:
- **Shortest Path**: BFS guarantees finding the shortest path between two vertices in an unweighted graph.
Completeness: BFS is complete, meaning it will always find a solution if one exists.
- **Optimal for Finding Shortest Path**: In unweighted graphs, BFS always finds the shortest path between two vertices.

### Disadvantage:
- **Memory Consumption**: BFS may consume more memory compared to DFS, especially in graphs with many vertices.
- **Slower in Dense Graphs**: BFS may be slower than DFS in dense graphs due to the larger memory footprint.

## Application
Breadth First Search finds applications in various fields, including:
- **Shortest Path Finding**: Used in GPS navigation systems to find the shortest route between two locations.
- **Network Broadcasting**: Used in network routing protocols to broadcast information to all nodes in a network.
- **Web Crawling**: BFS is used by search engines to crawl and index web pages on the internet.
- **Game Development**: In games like chess or tic-tac-toe, BFS is used to find the optimal move or path.
- **Social Network Analysis**: BFS is used to analyze social networks, such as finding friends of friends or shortest paths between users.
