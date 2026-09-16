# Data Structures & Algorithms (DSA) in JavaScript — Comprehensive Guide

This guide provides an end-to-end reference for Data Structures and Algorithms implemented natively in JavaScript (ES6+), following the 48-phase learning roadmap.

---

## Table of Contents
1. [JavaScript Fundamentals](#1-javascript-fundamentals)
2. [JS for DSA](#2-js-for-dsa)
3. [Time & Space Complexity](#3-time--space-complexity)
4. [Math & Number Theory](#4-math--number-theory)
5. [Recursion Basics](#5-recursion-basics)
6. [Arrays](#6-arrays)
7. [Strings](#7-strings)
8. [Hashing](#8-hashing)
9. [Two Pointers](#9-two-pointers)
10. [Sliding Window](#10-sliding-window)
11. [Prefix Sum](#11-prefix-sum)
12. [Sorting](#12-sorting)
13. [Advanced Sorting](#13-advanced-sorting)
14. [Binary Search](#14-binary-search)
15. [Binary Search on Answer](#15-binary-search-on-answer)
16. [Linked List](#16-linked-list)
17. [Stack](#17-stack)
18. [Queue](#18-queue)
19. [Hash Table](#19-hash-table)
20. [Recursion Advanced](#20-recursion-advanced)
21. [Backtracking](#21-backtracking)
22. [Trees](#22-trees)
23. [Tree Traversals](#23-tree-traversals)
24. [Binary Search Tree](#24-binary-search-tree)
25. [Heap / Priority Queue](#25-heap--priority-queue)
26. [Trie](#26-trie)
27. [Graph Basics](#27-graph-basics)
28. [BFS & DFS](#28-bfs--dfs)
29. [Graph Cycle Detection](#29-graph-cycle-detection)
30. [Topological Sort](#30-topological-sort)
31. [Shortest Path](#31-shortest-path)
32. [MST](#32-mst)
33. [Union Find](#33-union-find)
34. [Greedy](#34-greedy)
35. [Intervals](#35-intervals)
36. [Dynamic Programming Basics](#36-dynamic-programming-basics)
37. [1D DP](#37-1d-dp)
38. [2D DP](#38-2d-dp)
39. [Knapsack DP](#39-knapsack-dp)
40. [DP + Strings](#40-dp--strings)
41. [Bit Manipulation](#41-bit-manipulation)
42. [Advanced Data Structures](#42-advanced-data-structures)
43. [Advanced Graphs](#43-advanced-graphs)
44. [Advanced Algorithms](#44-advanced-algorithms)
45. [Interview Patterns](#45-interview-patterns)
46. [Mixed Problems](#46-mixed-problems)
47. [Mock Interviews](#47-mock-interviews)
48. [FAANG/MAANG Preparation](#48-faangmaang-preparation)

---

## 1. JavaScript Fundamentals
Basic programming constructs in JavaScript for problem solving: variables (`const`, `let`), primitive types, loops (`for`, `while`, `for...of`), conditionals, functions, and block scope.

```javascript
// Basic control structures
function isEven(num) {
  return num % 2 === 0;
}
```

---

## 2. JS for DSA
Key JavaScript objects and built-in features used for data structure implementations:
- Arrays: `[]`
- Key-Value Maps: `Map`
- Sets: `Set`
- Objects: `{}`
- Strings: Immutable sequences of UTF-16 code units

```javascript
const frequencyMap = new Map();
const uniqueElements = new Set([1, 2, 2, 3]);
```

---

## 3. Time & Space Complexity
Big-O notation measures algorithmic bounds as input size $N$ grows.

| Big-O | Name | Example |
| :--- | :--- | :--- |
| $O(1)$ | Constant | Array access by index, Map lookup |
| $O(\log N)$ | Logarithmic | Binary search, BST search (balanced) |
| $O(N)$ | Linear | Loop through array, Linear search |
| $O(N \log N)$ | Linearithmic | Merge Sort, Quick Sort (avg), Heap Sort |
| $O(N^2)$ | Quadratic | Nested loops, Bubble Sort, Insertion Sort |
| $O(2^N)$ | Exponential | Recursive Fibonacci without memoization |
| $O(N!)$ | Factorial | Generating all permutations of a string |

---

## 4. Math & Number Theory
Common algorithms involving numbers, prime testing, GCD, LCM, and modulo arithmetic.

```javascript
// Greatest Common Divisor (Euclidean Algorithm)
function gcd(a, b) {
  while (b) {
    [a, b] = [b, a % b];
  }
  return a;
}

// Sieve of Eratosthenes (Primes up to N)
function sieveOfEratosthenes(n) {
  const isPrime = new Array(n + 1).fill(true);
  isPrime[0] = isPrime[1] = false;
  for (let p = 2; p * p <= n; p++) {
    if (isPrime[p]) {
      for (let i = p * p; i <= n; i += p) {
        isPrime[i] = false;
      }
    }
  }
  return isPrime;
}
```

---

## 5. Recursion Basics
Breaking problems into smaller subproblems using base cases and call stacks.

```javascript
function factorial(n) {
  if (n <= 1) return 1; // Base case
  return n * factorial(n - 1);
}
```

---

## 6. Arrays
Linear collections offering contiguous memory allocation concepts and built-in operations.

```javascript
// Kadane's Algorithm for Maximum Subarray Sum
function maxSubArray(nums) {
  let maxSoFar = nums[0];
  let currentMax = nums[0];
  for (let i = 1; i < nums.length; i++) {
    currentMax = Math.max(nums[i], currentMax + nums[i]);
    maxSoFar = Math.max(maxSoFar, currentMax);
  }
  return maxSoFar;
}
```

---

## 7. Strings
Common operations including character traversal, substring extraction, sliding, and reverse logic.

```javascript
function isPalindrome(s) {
  const clean = s.toLowerCase().replace(/[^a-z0-9]/g, '');
  let left = 0, right = clean.length - 1;
  while (left < right) {
    if (clean[left++] !== clean[right--]) return false;
  }
  return true;
}
```

---

## 8. Hashing
Utilizing key-value pairs (`Map` or `{}`) and `Set` to reduce $O(N)$ lookup costs to $O(1)$ average time.

```javascript
function twoSum(nums, target) {
  const map = new Map();
  for (let i = 0; i < nums.length; i++) {
    const complement = target - nums[i];
    if (map.has(complement)) {
      return [map.get(complement), i];
    }
    map.set(nums[i], i);
  }
  return [];
}
```

---

## 9. Two Pointers
Iterating pointers from opposing ends or varying speeds across structured/sorted data.

```javascript
function twoSumSorted(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left < right) {
    const sum = arr[left] + arr[right];
    if (sum === target) return [left, right];
    if (sum < target) {
      left++;
    } else {
      right--;
    }
  }
  return [-1, -1];
}
```

---

## 10. Sliding Window
Maintaining a window frame over sequential data (fixed size or dynamic boundary).

```javascript
// Maximum sum subarray of size K (Fixed Window)
function maxSubarraySum(arr, k) {
  if (arr.length < k) return null;
  let maxSum = 0, windowSum = 0;
  for (let i = 0; i < k; i++) windowSum += arr[i];
  maxSum = windowSum;
  for (let i = k; i < arr.length; i++) {
    windowSum += arr[i] - arr[i - k];
    maxSum = Math.max(maxSum, windowSum);
  }
  return maxSum;
}

// Longest Substring Without Repeating Characters (Dynamic Window)
function lengthOfLongestSubstring(s) {
  const charMap = new Map();
  let maxLength = 0, left = 0;
  for (let right = 0; right < s.length; right++) {
    const char = s[right];
    if (charMap.has(char) && charMap.get(char) >= left) {
      left = charMap.get(char) + 1;
    }
    charMap.set(char, right);
    maxLength = Math.max(maxLength, right - left + 1);
  }
  return maxLength;
}
```

---

## 11. Prefix Sum
Precomputing cumulative sums to process range queries in $O(1)$ time.

```javascript
class NumArray {
  constructor(nums) {
    this.prefix = new Array(nums.length + 1).fill(0);
    for (let i = 0; i < nums.length; i++) {
      this.prefix[i + 1] = this.prefix[i] + nums[i];
    }
  }

  sumRange(left, right) {
    return this.prefix[right + 1] - this.prefix[left];
  }
}
```

---

## 12. Sorting
Elementary comparison-based sorting algorithms ($O(N^2)$ average/worst case).

```javascript
function bubbleSort(arr) {
  const n = arr.length;
  for (let i = 0; i < n; i++) {
    for (let j = 0; j < n - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        [arr[j], arr[j + 1]] = [arr[j + 1], arr[j]];
      }
    }
  }
  return arr;
}
```

---

## 13. Advanced Sorting
Divide and conquer and heap-based sorting algorithms ($O(N \log N)$ runtime).

```javascript
// Merge Sort
function mergeSort(arr) {
  if (arr.length <= 1) return arr;
  const mid = Math.floor(arr.length / 2);
  const left = mergeSort(arr.slice(0, mid));
  const right = mergeSort(arr.slice(mid));
  return merge(left, right);
}

function merge(left, right) {
  const result = [];
  let i = 0, j = 0;
  while (i < left.length && j < right.length) {
    if (left[i] <= right[j]) result.push(left[i++]);
    else result.push(right[j++]);
  }
  return [...result, ...left.slice(i), ...right.slice(j)];
}

// Quick Sort
function quickSort(arr) {
  if (arr.length <= 1) return arr;
  const pivot = arr[arr.length - 1];
  const left = [], right = [];
  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) left.push(arr[i]);
    else right.push(arr[i]);
  }
  return [...quickSort(left), pivot, ...quickSort(right)];
}
```

---

## 14. Binary Search
Dividing target search space in half each step ($O(\log N)$) on sorted data.

```javascript
function binarySearch(arr, target) {
  let left = 0, right = arr.length - 1;
  while (left <= right) {
    const mid = Math.floor(left + (right - left) / 2);
    if (arr[mid] === target) return mid;
    if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
  }
  return -1;
}
```

---

## 15. Binary Search on Answer
Applying binary search over a range of valid answers/parameters to find optimal boundary values.

```javascript
// Example: Find smallest divisor given a threshold
function smallestDivisor(nums, threshold) {
  let left = 1, right = Math.max(...nums);
  
  function computeSum(divisor) {
    return nums.reduce((sum, val) => sum + Math.ceil(val / divisor), 0);
  }

  while (left < right) {
    const mid = Math.floor(left + (right - left) / 2);
    if (computeSum(mid) <= threshold) {
      right = mid;
    } else {
      left = mid + 1;
    }
  }
  return left;
}
```

---

## 16. Linked List
Linear collections linked via node references.

```javascript
class ListNode {
  constructor(val = 0, next = null) {
    this.val = val;
    this.next = next;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
  }

  reverse() {
    let prev = null, curr = this.head;
    while (curr) {
      let nextTemp = curr.next;
      curr.next = prev;
      prev = curr;
      curr = nextTemp;
    }
    this.head = prev;
  }
}
```

---

## 17. Stack
Last-In, First-Out (LIFO) data structure and Monotonic Stack patterns.

```javascript
class Stack {
  constructor() {
    this.items = [];
  }
  push(element) { this.items.push(element); }
  pop() { return this.isEmpty() ? null : this.items.pop(); }
  peek() { return this.items[this.items.length - 1] || null; }
  isEmpty() { return this.items.length === 0; }
}

// Valid Parentheses
function isValidParentheses(s) {
  const stack = [];
  const map = { ')': '(', '}': '{', ']': '[' };
  for (const char of s) {
    if (char in map) {
      if (stack.pop() !== map[char]) return false;
    } else {
      stack.push(char);
    }
  }
  return stack.length === 0;
}
```

---

## 18. Queue
First-In, First-Out (FIFO) data structures and Deques (Double-Ended Queue).

```javascript
class QueueNode {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  enqueue(val) {
    const node = new QueueNode(val);
    if (!this.tail) {
      this.head = this.tail = node;
    } else {
      this.tail.next = node;
      this.tail = node;
    }
    this.size++;
  }

  dequeue() {
    if (!this.head) return null;
    const val = this.head.value;
    this.head = this.head.next;
    if (!this.head) this.tail = null;
    this.size--;
    return val;
  }
}
```

---

## 19. Hash Table
Implementation details behind hashing key-value mappings and handling collisions (separate chaining, open addressing).

```javascript
class SimpleHashTable {
  constructor(size = 53) {
    this.keyMap = new Array(size);
  }

  _hash(key) {
    let total = 0;
    const PRIME = 31;
    for (let i = 0; i < Math.min(key.length, 100); i++) {
      total = (total * PRIME + key.charCodeAt(i)) % this.keyMap.length;
    }
    return total;
  }

  set(key, value) {
    const index = this._hash(key);
    if (!this.keyMap[index]) this.keyMap[index] = [];
    this.keyMap[index].push([key, value]);
  }

  get(key) {
    const index = this._hash(key);
    if (this.keyMap[index]) {
      for (let pair of this.keyMap[index]) {
        if (pair[0] === key) return pair[1];
      }
    }
    return undefined;
  }
}
```

---

## 20. Recursion Advanced
Generating combinations, power sets, and sub-sequences using decision trees.

```javascript
function subsets(nums) {
  const result = [];
  function backtrack(index, path) {
    result.push([...path]);
    for (let i = index; i < nums.length; i++) {
      path.push(nums[i]);
      backtrack(i + 1, path);
      path.pop();
    }
  }
  backtrack(0, []);
  return result;
}
```

---

## 21. Backtracking
Systematic state-space search pruning dead ends when exploring constraints.

```javascript
function solveNQueens(n) {
  const result = [];
  const board = Array.from({ length: n }, () => Array(n).fill('.'));

  function isValid(row, col) {
    for (let i = 0; i < row; i++) {
      if (board[i][col] === 'Q') return false;
    }
    for (let i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
      if (board[i][j] === 'Q') return false;
    }
    for (let i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++) {
      if (board[i][j] === 'Q') return false;
    }
    return true;
  }

  function backtrack(row) {
    if (row === n) {
      result.push(board.map(r => r.join('')));
      return;
    }
    for (let col = 0; col < n; col++) {
      if (isValid(row, col)) {
        board[row][col] = 'Q';
        backtrack(row + 1);
        board[row][col] = '.';
      }
    }
  }

  backtrack(0);
  return result;
}
```

---

## 22. Trees
Hierarchical data structures formed by connected nodes with parent-child relationships.

```javascript
class TreeNode {
  constructor(val = 0, left = null, right = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

function maxDepth(root) {
  if (!root) return 0;
  return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```

---

## 23. Tree Traversals
Systematic techniques for visiting every node in a tree structure:
- **DFS**: Preorder (Root-L-R), Inorder (L-Root-R), Postorder (L-R-Root)
- **BFS**: Level-Order Traversal

```javascript
// Inorder Traversal (Recursive)
function inorderTraversal(root, result = []) {
  if (root) {
    inorderTraversal(root.left, result);
    result.push(root.val);
    inorderTraversal(root.right, result);
  }
  return result;
}

// Level Order Traversal (BFS)
function levelOrder(root) {
  const result = [];
  if (!root) return result;
  const queue = [root];
  while (queue.length > 0) {
    const levelSize = queue.length;
    const currentLevel = [];
    for (let i = 0; i < levelSize; i++) {
      const node = queue.shift();
      currentLevel.push(node.val);
      if (node.left) queue.push(node.left);
      if (node.right) queue.push(node.right);
    }
    result.push(currentLevel);
  }
  return result;
}
```

---

## 24. Binary Search Tree
Binary trees maintaining sorted order property where `left.val < root.val < right.val`.

```javascript
class BST {
  constructor() { this.root = null; }

  insert(val) {
    const newNode = new TreeNode(val);
    if (!this.root) { this.root = newNode; return; }
    let curr = this.root;
    while (true) {
      if (val < curr.val) {
        if (!curr.left) { curr.left = newNode; return; }
        curr = curr.left;
      } else {
        if (!curr.right) { curr.right = newNode; return; }
        curr = curr.right;
      }
    }
  }
}
```

---

## 25. Heap / Priority Queue
Complete binary trees optimized for retrieving minimum or maximum keys in $O(1)$ time and modifying in $O(\log N)$ time.

```javascript
class MinHeap {
  constructor() { this.heap = []; }
  getParentIndex(i) { return Math.floor((i - 1) / 2); }
  getLeftChildIndex(i) { return 2 * i + 1; }
  getRightChildIndex(i) { return 2 * i + 2; }
  swap(i1, i2) { [this.heap[i1], this.heap[i2]] = [this.heap[i2], this.heap[i1]]; }

  push(val) {
    this.heap.push(val);
    this.heapifyUp();
  }

  heapifyUp() {
    let index = this.heap.length - 1;
    while (index > 0 && this.heap[index] < this.heap[this.getParentIndex(index)]) {
      const pIdx = this.getParentIndex(index);
      this.swap(index, pIdx);
      index = pIdx;
    }
  }

  pop() {
    if (this.heap.length === 0) return null;
    if (this.heap.length === 1) return this.heap.pop();
    const item = this.heap[0];
    this.heap[0] = this.heap.pop();
    this.heapifyDown();
    return item;
  }

  heapifyDown() {
    let index = 0;
    while (this.getLeftChildIndex(index) < this.heap.length) {
      let smaller = this.getLeftChildIndex(index);
      const right = this.getRightChildIndex(index);
      if (right < this.heap.length && this.heap[right] < this.heap[smaller]) {
        smaller = right;
      }
      if (this.heap[index] <= this.heap[smaller]) break;
      this.swap(index, smaller);
      index = smaller;
    }
  }
}
```

---

## 26. Trie
Prefix tree data structure optimized for string retrieval and matching prefix lookups.

```javascript
class TrieNode {
  constructor() {
    this.children = {};
    this.isEndOfWord = false;
  }
}

class Trie {
  constructor() { this.root = new TrieNode(); }

  insert(word) {
    let curr = this.root;
    for (const char of word) {
      if (!curr.children[char]) curr.children[char] = new TrieNode();
      curr = curr.children[char];
    }
    curr.isEndOfWord = true;
  }

  search(word) {
    let curr = this.root;
    for (const char of word) {
      if (!curr.children[char]) return false;
      curr = curr.children[char];
    }
    return curr.isEndOfWord;
  }
}
```

---

## 27. Graph Basics
Graphs consisting of Vertices connected by Edges (Directed, Undirected, Weighted).

```javascript
class Graph {
  constructor() {
    this.adjacencyList = new Map();
  }

  addVertex(vertex) {
    if (!this.adjacencyList.has(vertex)) this.adjacencyList.set(vertex, []);
  }

  addEdge(v1, v2) {
    this.addVertex(v1);
    this.addVertex(v2);
    this.adjacencyList.get(v1).push(v2);
    this.adjacencyList.get(v2).push(v1);
  }
}
```

---

## 28. BFS & DFS
Fundamental graph traversal strategies.

```javascript
// Graph BFS
function bfs(graph, start) {
  const visited = new Set([start]);
  const queue = [start];
  while (queue.length > 0) {
    const node = queue.shift();
    for (const neighbor of graph.adjacencyList.get(node) || []) {
      if (!visited.has(neighbor)) {
        visited.add(neighbor);
        queue.push(neighbor);
      }
    }
  }
}
```

---

## 29. Graph Cycle Detection
Identifying cycles in directed (using recursion stack tracking) and undirected graphs (using parent pointers or Union-Find).

```javascript
// Undirected graph cycle detection using BFS
function hasCycleUndirected(graph, numVertices) {
  const visited = new Set();
  
  for (let i = 0; i < numVertices; i++) {
    if (visited.has(i)) continue;
    const queue = [[i, -1]]; // [node, parent]
    visited.add(i);

    while (queue.length > 0) {
      const [node, parent] = queue.shift();
      for (const neighbor of graph.adjacencyList.get(node) || []) {
        if (!visited.has(neighbor)) {
          visited.add(neighbor);
          queue.push([neighbor, node]);
        } else if (neighbor !== parent) {
          return true;
        }
      }
    }
  }
  return false;
}
```

---

## 30. Topological Sort
Linear ordering of vertices in Directed Acyclic Graphs (DAGs) such that for every edge $u \to v$, $u$ comes before $v$ (Kahn's Algorithm / DFS).

```javascript
function topologicalSort(numNodes, edges) {
  const inDegree = new Array(numNodes).fill(0);
  const adj = Array.from({ length: numNodes }, () => []);

  for (const [u, v] of edges) {
    adj[u].push(v);
    inDegree[v]++;
  }

  const queue = [];
  for (let i = 0; i < numNodes; i++) {
    if (inDegree[i] === 0) queue.push(i);
  }

  const order = [];
  while (queue.length > 0) {
    const curr = queue.shift();
    order.push(curr);
    for (const next of adj[curr]) {
      inDegree[next]--;
      if (inDegree[next] === 0) queue.push(next);
    }
  }

  return order.length === numNodes ? order : []; // Empty if cycle detected
}
```

---

## 31. Shortest Path
Finding shortest paths in graphs:
- Unweighted graph: BFS
- Weighted graph (positive edges): Dijkstra's Algorithm

```javascript
function dijkstra(graph, start) {
  const distances = {};
  const pq = new MinHeap(); // Priority queue stores [distance, node]
  
  for (const vertex of graph.adjacencyList.keys()) {
    distances[vertex] = Infinity;
  }
  distances[start] = 0;
  pq.push({ node: start, dist: 0 });

  while (pq.heap.length > 0) {
    const { node, dist } = pq.pop();
    if (dist > distances[node]) continue;

    for (const neighbor of graph.adjacencyList.get(node) || []) {
      const newDist = distances[node] + neighbor.weight;
      if (newDist < distances[neighbor.node]) {
        distances[neighbor.node] = newDist;
        pq.push({ node: neighbor.node, dist: newDist });
      }
    }
  }
  return distances;
}
```

---

## 32. MST
Minimum Spanning Trees connect all graph vertices together with minimum edge weight sum (Kruskal's Algorithm, Prim's Algorithm).

```javascript
function kruskal(numNodes, edges) {
  // edges: [[u, v, weight]]
  edges.sort((a, b) => a[2] - b[2]);
  const dsu = new UnionFind(numNodes);
  let mstWeight = 0, count = 0;

  for (const [u, v, w] of edges) {
    if (dsu.union(u, v)) {
      mstWeight += w;
      count++;
      if (count === numNodes - 1) break;
    }
  }
  return mstWeight;
}
```

---

## 33. Union Find
Disjoint Set Union (DSU) tracking partitioned sets with Path Compression and Union by Rank.

```javascript
class UnionFind {
  constructor(size) {
    this.parent = Array.from({ length: size }, (_, i) => i);
    this.rank = new Array(size).fill(0);
  }

  find(i) {
    if (this.parent[i] === i) return i;
    this.parent[i] = this.find(this.parent[i]); // Path compression
    return this.parent[i];
  }

  union(i, j) {
    const rootI = this.find(i);
    const rootJ = this.find(j);
    if (rootI !== rootJ) {
      if (this.rank[rootI] < this.rank[rootJ]) this.parent[rootI] = rootJ;
      else if (this.rank[rootI] > this.rank[rootJ]) this.parent[rootJ] = rootI;
      else {
        this.parent[rootJ] = rootI;
        this.rank[rootI]++;
      }
      return true;
    }
    return false;
  }
}
```

---

## 34. Greedy
Making locally optimal choices at each stage to produce globally optimal solutions.

```javascript
function coinChangeGreedy(coins, amount) {
  coins.sort((a, b) => b - a);
  let count = 0, remaining = amount;
  for (const coin of coins) {
    if (remaining === 0) break;
    count += Math.floor(remaining / coin);
    remaining %= coin;
  }
  return remaining === 0 ? count : -1;
}
```

---

## 35. Intervals
Problems involving sorting, merging, and determining overlap between bounded intervals.

```javascript
function mergeIntervals(intervals) {
  if (!intervals.length) return [];
  intervals.sort((a, b) => a[0] - b[0]);
  const result = [intervals[0]];

  for (let i = 1; i < intervals.length; i++) {
    const last = result[result.length - 1];
    const curr = intervals[i];
    if (curr[0] <= last[1]) {
      last[1] = Math.max(last[1], curr[1]);
    } else {
      result.push(curr);
    }
  }
  return result;
}
```

---

## 36. Dynamic Programming Basics
Solving optimization problems by combining solutions to overlapping subproblems (Memoization & Tabulation).

```javascript
// Climbing Stairs (Tabulation)
function climbStairs(n) {
  if (n <= 2) return n;
  let prev1 = 1, prev2 = 2;
  for (let i = 3; i <= n; i++) {
    const curr = prev1 + prev2;
    prev1 = prev2;
    prev2 = curr;
  }
  return prev2;
}
```

---

## 37. 1D DP
Linear Dynamic Programming state formulations ($DP[i]$ depending on previous indices).

```javascript
// Coin Change (1D DP)
function coinChange(coins, amount) {
  const dp = new Array(amount + 1).fill(Infinity);
  dp[0] = 0;
  for (let i = 1; i <= amount; i++) {
    for (const coin of coins) {
      if (i - coin >= 0) {
        dp[i] = Math.min(dp[i], dp[i - coin] + 1);
      }
    }
  }
  return dp[amount] === Infinity ? -1 : dp[amount];
}
```

---

## 38. 2D DP
Grid or double-sequence state formulations ($DP[i][j]$).

```javascript
// Unique Paths in Grid
function uniquePaths(m, n) {
  const dp = Array.from({ length: m }, () => Array(n).fill(1));
  for (let i = 1; i < m; i++) {
    for (let j = 1; j < n; j++) {
      dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
    }
  }
  return dp[m - 1][n - 1];
}
```

---

## 39. Knapsack DP
0/1, Unbounded, and Subset-Sum DP problems.

```javascript
function knapsack01(weights, values, capacity) {
  const n = weights.length;
  const dp = Array.from({ length: n + 1 }, () => Array(capacity + 1).fill(0));

  for (let i = 1; i <= n; i++) {
    for (let w = 0; w <= capacity; w++) {
      if (weights[i - 1] <= w) {
        dp[i][w] = Math.max(dp[i - 1][w], dp[i - 1][w - weights[i - 1]] + values[i - 1]);
      } else {
        dp[i][w] = dp[i - 1][w];
      }
    }
  }
  return dp[n][capacity];
}
```

---

## 40. DP + Strings
Dynamic programming applied to string matching, editing, and palindrome partitioning.

```javascript
// Longest Common Subsequence
function longestCommonSubsequence(text1, text2) {
  const m = text1.length, n = text2.length;
  const dp = Array.from({ length: m + 1 }, () => Array(n + 1).fill(0));

  for (let i = 1; i <= m; i++) {
    for (let j = 1; j <= n; j++) {
      if (text1[i - 1] === text2[j - 1]) {
        dp[i][j] = dp[i - 1][j - 1] + 1;
      } else {
        dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
      }
    }
  }
  return dp[m][n];
}
```

---

## 41. Bit Manipulation
Bitwise operations (`AND`, `OR`, `XOR`, `NOT`, bit shifts) for fast binary processing.

```javascript
// Single Number (XOR Property)
function singleNumber(nums) {
  let result = 0;
  for (const num of nums) {
    result ^= num;
  }
  return result;
}
```

---

## 42. Advanced Data Structures
Tree-based range query structures: Segment Trees and Binary Indexed Trees (Fenwick Trees).

```javascript
class NumArraySegmentTree {
  constructor(nums) {
    this.n = nums.length;
    this.tree = new Array(2 * this.n).fill(0);
    for (let i = 0; i < this.n; i++) this.tree[this.n + i] = nums[i];
    for (let i = this.n - 1; i > 0; i--) this.tree[i] = this.tree[2 * i] + this.tree[2 * i + 1];
  }

  update(index, val) {
    let pos = index + this.n;
    this.tree[pos] = val;
    while (pos > 1) {
      pos = Math.floor(pos / 2);
      this.tree[pos] = this.tree[2 * pos] + this.tree[2 * pos + 1];
    }
  }

  sumRange(left, right) {
    let l = left + this.n, r = right + this.n;
    let sum = 0;
    while (l <= r) {
      if (l % 2 === 1) sum += this.tree[l++];
      if (r % 2 === 0) sum += this.tree[r--];
      l = Math.floor(l / 2);
      r = Math.floor(r / 2);
    }
    return sum;
  }
}
```

---

## 43. Advanced Graphs
Shortest path algorithms handling negative edge weights and all-pairs paths: Bellman-Ford and Floyd-Warshall.

```javascript
// Bellman-Ford Algorithm
function bellmanFord(numNodes, edges, start) {
  const dist = new Array(numNodes).fill(Infinity);
  dist[start] = 0;

  for (let i = 0; i < numNodes - 1; i++) {
    for (const [u, v, w] of edges) {
      if (dist[u] !== Infinity && dist[u] + w < dist[v]) {
        dist[v] = dist[u] + w;
      }
    }
  }
  return dist;
}
```

---

## 44. Advanced Algorithms
Pattern matching algorithms for string search in $O(N + M)$ time (Knuth-Morris-Pratt and Rabin-Karp).

```javascript
// KMP Prefix Table Helper
function buildLPSArray(pattern) {
  const lps = new Array(pattern.length).fill(0);
  let len = 0, i = 1;
  while (i < pattern.length) {
    if (pattern[i] === pattern[len]) {
      len++;
      lps[i] = len;
      i++;
    } else {
      if (len !== 0) len = lps[len - 1];
      else { lps[i] = 0; i++; }
    }
  }
  return lps;
}
```

---

## 45. Interview Patterns
Recognizing top algorithmic patterns quickly in technical interviews:
- Two Pointers
- Fast & Slow Pointers
- Sliding Window
- Monotonic Stack
- Top K Elements
- Overlapping Intervals

---

## 46. Mixed Problems
Solving complex LeetCode Medium/Hard challenges that combine multiple DSA techniques simultaneously.

---

## 47. Mock Interviews
Strategies for timed 45–60 minute technical interviews:
1. Clarify edge cases and constraints
2. Explain brute-force before optimizing
3. Trace sample inputs dry-run style
4. Write clean, bug-free production code
5. Analyze time and space complexity

---

## 48. FAANG/MAANG Preparation
High-frequency company-style problems, code refinement, system performance considerations, and edge case hardening.
