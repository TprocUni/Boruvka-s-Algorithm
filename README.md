# Boruvka-s-Algorithm
here we Notebook implements **Borůvka’s algorithm** for finding the Minimum Spanning Tree (MST) of a graph. It iteratively merges graph components with the minimum edge between them until a connected MST or forest is formed. OpenMP parallelization is used to improve performance in handling large graphs.



Borůvka's algorithm is a **greedy algorithm** used to find the Minimum Spanning Tree (MST) of a graph. It works by iteratively merging components (connected subgraphs) with the minimum edge between them until all nodes are connected in a single tree with minimal total edge weight. This notebook implements Borůvka's algorithm on a graph structure, providing functions to manage nodes, edges, and components.

#### 1. Graph Representation and Setup

The notebook defines a `Graph` class to represent the graph structure, which includes:

- **Nodes**: Represented by unique integer IDs, with each node initially assigned to its own component.
- **Edges**: Each edge connects two nodes with a specified weight, indicating the cost or distance between them.
- **Components**: Each node starts in its own component, which merges with other components during the algorithm's execution.

The `Graph` class has several methods:

1. **`makeEdge`**: Adds an edge between two nodes with a specified weight.
2. **`showEdge`**: Displays the details of a specific edge.
3. **`findComp`**: Recursively finds the root component of a node, enabling path compression, which speeds up the algorithm.
4. **`setComp`**: Updates component values by ensuring all nodes in a component point to the root node.

These helper functions set up the framework for managing edges and components, essential for tracking which nodes are already connected and ensuring no cycles are formed.

#### 2. Borůvka’s Algorithm Implementation

The **`boruvkaAlgorithm`** method is the core of the notebook and contains the following main steps:

1. **Initial Setup**:
   - The algorithm initializes each node as its own component, and each component has an initial edge weight of `-1` (indicating no edge selected).
   - Variables for component size (`compSize`), graph weight (`graphWeight`), and component count (`compNum`) are initialized.

2. **Main Loop**:
   - The main loop runs until the number of components (`compNum`) is reduced to 1 or the graph is confirmed as a forest (disconnected parts).
   - In each iteration:
     - For each edge, the algorithm checks if it connects two different components and, if so, compares the edge weight to the current minimum edge for those components.
     - The smallest edges for each component are stored, forming a list of edges that will be added in this iteration.
   - After determining the minimum edge for each component, the algorithm merges components based on these edges, updating the graph weight and reducing the component count (`compNum`).

3. **Component Merging**:
   - The **`combine`** method merges two components based on their sizes to balance the tree structure, optimizing future component lookups.
   - The components of nodes are updated to reflect the new merged structure, ensuring efficient component tracking as the algorithm progresses.

4. **Checking for Forest Structure**:
   - If the number of components remains unchanged after an iteration, the algorithm detects a "forest," meaning the graph has disconnected parts that cannot be further connected.
   - In this case, it reports the MST weight and the number of components in the resulting forest.

#### 3. Output and Visualization

- **MST Weight**: At the end of the algorithm, the total weight of the MST is printed, showing the minimum sum of edge weights required to connect all nodes in a tree.
- **Component Count**: If the graph is a forest, the algorithm outputs the number of components remaining, indicating that a complete MST cannot be formed.
- **Edge Details**: For each edge added to the MST, the algorithm prints which nodes are connected and the edge's weight, providing a step-by-step view of the MST construction.

#### 4. Performance and Complexity

Borůvka's algorithm operates efficiently in parallelizable stages, with each stage reducing the number of components by merging components via the shortest available edges. The algorithm's complexity is `O(E log V)`, where `E` is the number of edges and `V` is the number of vertices. This implementation, while simple, highlights key optimization steps such as path compression in `findComp`, which enhances performance by reducing redundant component lookups.

#### Summary

This notebook effectively implements Borůvka's algorithm for MST construction on an undirected graph. It initializes a graph with edges and nodes, then iteratively finds and merges components using the minimum connecting edges until all nodes are connected or a forest is formed. The algorithm’s output includes the MST weight, detailed edge connections, and component count in the case of a forest structure. This implementation demonstrates fundamental graph theory concepts, particularly in component merging and efficient MST construction.











