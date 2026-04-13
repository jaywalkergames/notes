### Array

A collection of items stored in contiguous memory locations.

Insert: O(N)

Remove: O(N)

Access: O(1)

Search: O(N)

Sort: O(NlogN)

### Hash Table

An array index by a hashed value. An effective hashing function allows the hash table O(1) amortized operations. A hashing function also allows the creation of non-integer indices to array.

Insert: O(1)

Remove: O(1)

Access: O(1)

Search: O(1)

Sort: O(NlogN)

### Linked-list

A collection of items stored in contiguous memory locations.

Insert: O(1)

Remove: O(1)

Search: O(N)

Sort: O(NlogN)

### Stack

LIFO

### Queue

FIFO

### Priority Queue

A collection of items stored in contiguous memory locations.

### Binary Tree

A tree data structure where each node has at most 2 children and 1 parent.

### Binary Search Tree

A binary tree where the node values increase from left to right. Traversals in O(N) time and O(logN) space.

In-order traversal: Traverse tree from smallest to largest element.

Pre-order traversal: Staring at root, visit left subtree, then right subtree.

Post-order traversal: Traverse left subtree, then right subtree, then root.

### Red-Black Tree

A balanced binary search tree that guarantees O(logn) insertion, deletion, and searching.

1. Root property: The root is black.
2. External property: Every leaf is black
3. Internal property: The children of red nodes are black
4. Depth property: All leaves have the same depth
5. Path property: Every path from root to leaf contains the same number of black nodes

Insert: O(logN)

Remove: O(logN)

Search: O(logN)

Sort: O(N)

### Heap

A complete (all levels are filled except the lowest) binary tree

### Binary Heap

A heap where the root is the minimum (Min Heap) or maximum (Max Heap) node.

Insert: O(logN)

Remove: O(logN)

Search: O(N)

Sort: O(NlogN)

Union: O(N)

Find-min: O(1)

Decrease-key: O(logN)

### Binomial Heap

A set of binary heaps whose roots are in a linked list (used in implementing priority queue).

Insert: O(logN)

Remove: O(logN)

Search: O(N)

Sort: O(NlogN)

Union: O(logN)

Find-min: O(logN)

Decrease-key: O(logN)

### Fibonacci Heap

A collection of heap-ordered trees. Inserting adds the new node to the root list. Deleting a node moves its children to the root lists and consolidates until there are no nodes at the same level with the same number of children.

Insert: O(1)

Remove: O(logN)

Search: O(N)

Sort: O(NlogN)

Union: O(1)

Find-min: O(1)

Decrease-key: O(1)

### Adjacency List

An array of linked lists. The first element of each list represents the node in the graph and each connected element represents an edge to that node in the graph. Use for sparse graphs or graphs whose contents change often.

Space: O(V+E)

Search Edge: O(V)

Add Vertex: O(1)

Add Edge: O(1)

Remove Vertex: O(V+E)

Remove Edge: O(E)

### Adjacency Matrix

A 2D array where N is the number of nodes in the graph. The value at element adj_matrix[i][j] represents the weight of the edge of the graph between the nodes. Use for dense graphs or graphs that frequently access specific edges.

Space: O(V^2)

Search Edge: O(1)

Add Vertex: O(V^2)

Add Edge: O(1)

Remove Vertex: O(V^2)

Remove Edge: O(1)

### Tries

A tree where each node is a hashmap of pointers. Each index in the hashmap represents a character and a flag to indicate if any string ends at the current node. Each path from the root node to any node represents a word or string.

Space: O(NML)

Search: O(M)

Add Word: O(M)

Delete Word: O(M)

### Divide and Conquer Algorithms

1. Divide a problem into smaller sub-problems
2. Solve the sub-problems recursively
3. Combine the solutions to the sub-problems

### Greedy Algorithms

Make the locally optimal choice at each stage

Structure

1. Structure problem as an optimization problem
2. Determine possible solution set
3. Determine optimal substructure of the problem
4. Take the locally optimal solution at each sub-problem

### Dynamic Programming Algorithms

Use tabulation or memoization

- Tabulation (bottom-up): solve problems by storing results of sub-problems
- Memozation (top-down): cache results of function calls

Structure

1. Structure problem as sub-problem with overlapping solutions
2. Create state-transition diagram
3. Implement tabulation or memoization

### Backtracking Algorithms

Incrementally solve a problem. Re-curse to fork if dead-end is found.

### Branch and Bound Algorithms

Assign bound to each possible node and going down those paths. Unlike backtracking, it dismisses a search path when:

1. The bound value of a node is lower than the upper bound.
2. The node represents infeasible solution.
3. The node is a subset of a feasible solution containing a single point.

### Randomized Algorithms

Use random numbers to decide what to do next in its logic

- Monte Carlo algorithms use repeated random sampling to compute their results
- Quick sort can use a randomized pivot

### Bitwise

- Left shift (x<<): Multiply a number by 2
- Right shift (x>>): Divide a number by 2

### Rabin-Karp Pattern Matching

Time: O(n+m)

Space: O(1)

Steps

1. Iterate through the string
2. Computer hash value of each sub-string of equal length to pattern
3. Compare hash value to hash value of pattern

### Aho Coraisic Pattern Matching

Time: O(n+m+z) where z is the number of matches

Space: O(m*q) where q is the length of the alphabet

Steps

1. Build a trie of pattern(s)
    - Fills entries in goto g[][] and output o[]
2. Build an automaton for linear time matching
    - Fills entries in failure f[] and output o[]
3. Complete
    - Goto: Build trie, all chars that don't have an edge at root, add edge back to root
    - Failure: find longest proper suffix of some pattern for each state using BFS of Trie
    - Output: Store indices of all words ending at s as a bitwise map using BFS if Failure
4. Traverse text over built automaton to find all matching words

- Goto: Follows edges of a Trie of all patterns. Represented as 2D array where each element is the next state for the current state.
- Failure: stores edges that are followed when the current character doesn't have an edge in goto. 1D array where each element is the next state for the current state.
- Output: stores indices of all words that end at current state. 1D array where each element is all matching words as a bitmap of starting indices.

## Graph Algorithms

### Breadth First Search

Traversal of graph starting at the root of the graph and visiting all unvisited nodes at the current depth before moving on. If a neighbor of the current node in the queue is unvisited, add it to the end of the queue.

Time: O(V+E)

Space: O(V)

### Depth First Search

Traversal of graph starting at the root of the graph and visiting all unvisted nodes of a branch before backtracking. If a neigbor of the current node at the end of the stack is unvisited, add it to the stack.

Time: O(V+E)

Space: O(V+E)

### Dijkstra's Single Source Shortest Path

Steps:

1. Mark the source node with a current distance of 0 and the rest with infinity.
2. Set the non-visited node with the smallest current distance as the current node.
3. For each neighbor, N of the current node adds the current distance of the adjacent node with the weight of the edge connecting 0->1. If it is smaller than the current distance of Node, set it as the new current distance of N.
4. Mark the current node 1 as visited.
5. Go to step 2 if there are any nodes are unvisited.

Time: O(ElogV) with priority queue

Space: O(V^2) with priority queue

### Johnson's All Pairs Shortest Path

Reweight a graph to all positive edge weights and apply Dijkstra's SSSP to every node.

Time: O(V^2logV+VE)

Space: O(V^2)
