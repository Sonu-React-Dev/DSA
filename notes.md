# Data Structures & Algorithms (DSA) in JavaScript — Comprehensive Guide

This guide provides an end-to-end reference for Data Structures and Algorithms implemented natively in JavaScript (ES6+).

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

## 1. Big-O Notation & Complexity Analysis

Big-O measures the upper bound of runtime or space required by an algorithm as input size $N$ grows.

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

## 2. JavaScript Data Structure Cheat Sheet

| Data Structure | Built-in JS Equivalent | Time: Access | Time: Search | Time: Insert | Time: Delete |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Array** | `[]` | $O(1)$ | $O(N)$ | $O(1)$ end / $O(N)$ start | $O(1)$ end / $O(N)$ start |
| **Stack** | `[]` (push/pop) | $O(N)$ | $O(N)$ | $O(1)$ | $O(1)$ |
| **Queue** | Custom LinkedList / Array | $O(N)$ | $O(N)$ | $O(1)$ | $O(1)$ (LinkedList) / $O(N)$ (Array `shift`) |
| **Linked List** | Custom Class | $O(N)$ | $O(N)$ | $O(1)$ (known node) | $O(1)$ (known node) |
| **Hash Table** | `Map` or `{}` | N/A | $O(1)$ avg | $O(1)$ avg | $O(1)$ avg |
| **Set** | `Set` | N/A | $O(1)$ avg | $O(1)$ avg | $O(1)$ avg |
| **BST** | Custom Class | $O(\log N)$ | $O(\log N)$ | $O(\log N)$ | $O(\log N)$ |
| **Min/Max Heap** | Custom Class | $O(1)$ (min/max) | $O(N)$ | $O(\log N)$ | $O(\log N)$ |

---

## 3. Linear Data Structures

### Arrays & Strings
JavaScript arrays are dynamic. Useful methods for DSA:
- `push()`, `pop()`: $O(1)$
- `shift()`, `unshift()`: $O(N)$
- `splice()`: $O(N)$
- `slice()`: $O(N)$

---

### Stacks
Last-In, First-Out (LIFO).

```javascript
class Stack {
  constructor() {
    this.items = [];
  }

  push(element) {
    this.items.push(element);
  }

  pop() {
    if (this.isEmpty()) return null;
    return this.items.pop();
  }

  peek() {
    return this.items[this.items.length - 1] || null;
  }

  isEmpty() {
    return this.items.length === 0;
  }

  size() {
    return this.items.length;
  }
}
```

---

### Queues & Deques
First-In, First-Out (FIFO). Using a Linked List for $O(1)$ operations:

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

  peek() {
    return this.head ? this.head.value : null;
  }

  isEmpty() {
    return this.size === 0;
  }
}
```

### Deque (Double-Ended Queue)
A deque allows insertion and deletion from both ends in O(1) time.

```javascript
class DequeNode {
  constructor(value) {
    this.value = value;
    this.prev = null;
    this.next = null;
  }
}

class Deque {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  // Add to front
  addFront(value) {
    const node = new DequeNode(value);
    if (!this.head) {
      this.head = this.tail = node;
    } else {
      node.next = this.head;
      this.head.prev = node;
      this.head = node;
    }
    this.size++;
  }

  // Add to back
  addBack(value) {
    const node = new DequeNode(value);
    if (!this.tail) {
      this.head = this.tail = node;
    } else {
      this.tail.next = node;
      node.prev = this.tail;
      this.tail = node;
    }
    this.size++;
  }

  // Remove from front
  removeFront() {
    if (!this.head) return null;
    const value = this.head.value;
    this.head = this.head.next;
    if (this.head) {
      this.head.prev = null;
    } else {
      this.tail = null;
    }
    this.size--;
    return value;
  }

  // Remove from back
  removeBack() {
    if (!this.tail) return null;
    const value = this.tail.value;
    this.tail = this.tail.prev;
    if (this.tail) {
      this.tail.next = null;
    } else {
      this.head = null;
    }
    this.size--;
    return value;
  }

  // Peek front
  peekFront() {
    return this.head ? this.head.value : null;
  }

  // Peek back
  peekBack() {
    return this.tail ? this.tail.value : null;
  }

  isEmpty() {
    return this.size === 0;
  }

  getSize() {
    return this.size;
  }
}
```

---

### Singly & Doubly Linked Lists

#### Singly Linked List Implementation:
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
    this.size = 0;
  }

  insertAtHead(val) {
    this.head = new ListNode(val, this.head);
    this.size++;
  }

  insertAtTail(val) {
    const newNode = new ListNode(val);
    if (!this.head) {
      this.head = newNode;
    } else {
      let current = this.head;
      while (current.next) {
        current = current.next;
      }
      current.next = newNode;
    }
    this.size++;
  }

  reverse() {
    let prev = null;
    let curr = this.head;
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

##### Doubly Linked List Implementation
```javascript
class DListNode {
  constructor(val, prev = null, next = null) {
    this.val = val;
    this.prev = prev;
    this.next = next;
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  append(val) {
    const newNode = new DListNode(val);
    if (!this.head) {
      this.head = this.tail = newNode;
    } else {
      this.tail.next = newNode;
      newNode.prev = this.tail;
      this.tail = newNode;
    }
    this.size++;
  }

  prepend(val) {
    const newNode = new DListNode(val);
    if (!this.head) {
      this.head = this.tail = newNode;
    } else {
      newNode.next = this.head;
      this.head.prev = newNode;
      this.head = newNode;
    }
    this.size++;
  }

  getSize() {
    return this.size;
  }

  contains(val) {
    let current = this.head;
    while (current) {
      if (current.val === val) return true;
      current = current.next;
    }
    return false;
  }
}
```

---

## 4. Non-Linear Data Structures

### Hash Tables (Objects & Maps)
Use `Map` when keys are non-strings or order matters, or when frequent insertions/deletions occur.

```javascript
const map = new Map();
map.set('key', 'value'); // O(1)
map.get('key');        // O(1)
map.has('key');        // O(1)
map.delete('key');     // O(1)
```

---

### Trees & Binary Search Trees (BST)

```javascript
class TreeNode {
  constructor(val = 0, left = null, right = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

class BinarySearchTree {
  constructor() {
    this.root = null;
  }

  insert(val) {
    const newNode = new TreeNode(val);
    if (!this.root) {
      this.root = newNode;
      return;
    }
    let current = this.root;
    while (true) {
      if (val < current.val) {
        if (!current.left) {
          current.left = newNode;
          return;
        }
        current = current.left;
      } else {
        if (!current.right) {
          current.right = newNode;
          return;
        }
        current = current.right;
      }
    }
  }

  // In-order traversal: Left -> Node -> Right (Sorted order for BST)
  inOrder(node = this.root, result = []) {
    if (node) {
      this.inOrder(node.left, result);
      result.push(node.val);
      this.inOrder(node.right, result);
    }
    return result;
  }

  // Level-order traversal (BFS)
  bfs() {
    const result = [];
    if (!this.root) return result;
    const queue = [this.root];
    while (queue.length > 0) {
      const current = queue.shift();
      result.push(current.val);
      if (current.left) queue.push(current.left);
      if (current.right) queue.push(current.right);
    }
    return result;
  }
}
```

---

### Binary Heaps & Priority Queues

Min-Heap implementation:
```javascript
class MinHeap {
  constructor() {
    this.heap = [];
  }

  getParentIndex(i) { return Math.floor((i - 1) / 2); }
  getLeftChildIndex(i) { return 2 * i + 1; }
  getRightChildIndex(i) { return 2 * i + 2; }

  swap(i1, i2) {
    [this.heap[i1], this.heap[i2]] = [this.heap[i2], this.heap[i1]];
  }

  push(val) {
    this.heap.push(val);
    this.heapifyUp();
  }

  heapifyUp() {
    let index = this.heap.length - 1;
    while (
      index > 0 &&
      this.heap[index] < this.heap[this.getParentIndex(index)]
    ) {
      const parentIdx = this.getParentIndex(index);
      this.swap(index, parentIdx);
      index = parentIdx;
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
      let smallerChildIndex = this.getLeftChildIndex(index);
      const rightChildIdx = this.getRightChildIndex(index);
      if (
        rightChildIdx < this.heap.length &&
        this.heap[rightChildIdx] < this.heap[smallerChildIndex]
      ) {
        smallerChildIndex = rightChildIdx;
      }

      if (this.heap[index] <= this.heap[smallerChildIndex]) break;

      this.swap(index, smallerChildIndex);
      index = smallerChildIndex;
    }
  }

  peek() {
    return this.heap[0] || null;
  }
}
```

### Priority Queue
Built on top of the Min-Heap, a Priority Queue dequeues elements by priority.

```javascript
class PriorityQueue {
  constructor(comparator = (a, b) => a - b) {
    this.heap = [];
    this.compare = comparator;
  }

  getParentIndex(i) { return Math.floor((i - 1) / 2); }
  getLeftChildIndex(i) { return 2 * i + 1; }
  getRightChildIndex(i) { return 2 * i + 2; }

  swap(i1, i2) {
    [this.heap[i1], this.heap[i2]] = [this.heap[i2], this.heap[i1]];
  }

  size() {
    return this.heap.length;
  }

  isEmpty() {
    return this.heap.length === 0;
  }

  peek() {
    return this.heap[0] || null;
  }

  push(val) {
    this.heap.push(val);
    this.heapifyUp();
  }

  heapifyUp() {
    let index = this.heap.length - 1;
    while (
      index > 0 &&
      this.compare(this.heap[index], this.heap[this.getParentIndex(index)]) < 0
    ) {
      const parentIdx = this.getParentIndex(index);
      this.swap(index, parentIdx);
      index = parentIdx;
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
      let priorityChildIndex = this.getLeftChildIndex(index);
      const rightChildIdx = this.getRightChildIndex(index);
      if (
        rightChildIdx < this.heap.length &&
        this.compare(this.heap[rightChildIdx], this.heap[priorityChildIndex]) < 0
      ) {
        priorityChildIndex = rightChildIdx;
      }

      if (this.compare(this.heap[index], this.heap[priorityChildIndex]) <= 0) break;

      this.swap(index, priorityChildIndex);
      index = priorityChildIndex;
    }
  }
}
```

---

### Graphs
Represented using Adjacency List:

```javascript
class Graph {
  constructor() {
    this.adjacencyList = new Map();
  }

  addVertex(vertex) {
    if (!this.adjacencyList.has(vertex)) {
      this.adjacencyList.set(vertex, []);
    }
  }

  addEdge(v1, v2) {
    this.addVertex(v1);
    this.addVertex(v2);
    this.adjacencyList.get(v1).push(v2);
    this.adjacencyList.get(v2).push(v1); // Undirected graph
  }

  bfs(start) {
    const visited = new Set([start]);
    const queue = [start];
    const result = [];

    while (queue.length > 0) {
      const vertex = queue.shift();
      result.push(vertex);

      for (const neighbor of this.adjacencyList.get(vertex) || []) {
        if (!visited.has(neighbor)) {
          visited.add(neighbor);
          queue.push(neighbor);
        }
      }
    }
    return result;
  }

  dfs(start) {
    const visited = new Set();
    const result = [];
    const adj = this.adjacencyList;

    function traverse(vertex) {
      if (!vertex) return;
      visited.add(vertex);
      result.push(vertex);

      for (const neighbor of adj.get(vertex) || []) {
        if (!visited.has(neighbor)) {
          traverse(neighbor);
        }
      }
    }

    traverse(start);
    return result;
  }
}
```

---

### Tries (Prefix Trees)

```javascript
class TrieNode {
  constructor() {
    this.children = {};
    this.isEndOfWord = false;
  }
}

class Trie {
  constructor() {
    this.root = new TrieNode();
  }

  insert(word) {
    let current = this.root;
    for (const char of word) {
      if (!current.children[char]) {
        current.children[char] = new TrieNode();
      }
      current = current.children[char];
    }
    current.isEndOfWord = true;
  }

  search(word) {
    let current = this.root;
    for (const char of word) {
      if (!current.children[char]) return false;
      current = current.children[char];
    }
    return current.isEndOfWord;
  }

  startsWith(prefix) {
    let current = this.root;
    for (const char of prefix) {
      if (!current.children[char]) return false;
      current = current.children[char];
    }
    return true;
  }
}
```

---

### Disjoint Set Union (DSU / Union-Find)

```javascript
class UnionFind {
  constructor(size) {
    this.parent = Array.from({ length: size }, (_, i) => i);
    this.rank = new Array(size).fill(0);
  }

  find(i) {
    if (this.parent[i] === i) return i;
    // Path compression
    this.parent[i] = this.find(this.parent[i]);
    return this.parent[i];
  }

  union(i, j) {
    const rootI = this.find(i);
    const rootJ = this.find(j);

    if (rootI !== rootJ) {
      // Union by rank
      if (this.rank[rootI] < this.rank[rootJ]) {
        this.parent[rootI] = rootJ;
      } else if (this.rank[rootI] > this.rank[rootJ]) {
        this.parent[rootJ] = rootI;
      } else {
        this.parent[rootJ] = rootI;
        this.rank[rootI]++;
      }
      return true;
    }
    return false; // Already in same set (cycle detected)
  }
}
```


---

## 5. Core Algorithmic Patterns

### Two Pointers
Used for sorted arrays, searching pairs, or reversing elements in $O(N)$ time with $O(1)$ space.

```javascript
// Target Sum in a Sorted Array
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

### Sliding Window
Used for contiguous subarray or substring problems (fixed or dynamic window size).

```javascript
// Maximum sum subarray of size K (Fixed Window)
function maxSubarraySum(arr, k) {
  if (arr.length < k) return null;

  let maxSum = 0;
  let windowSum = 0;

  for (let i = 0; i < k; i++) {
    windowSum += arr[i];
  }
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
  let maxLength = 0;
  let left = 0;

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

### Fast & Slow Pointers (Floyd's Cycle)
Used to detect cycles in linked lists or find the middle node in a single pass.

```javascript
function hasCycle(head) {
  let slow = head;
  let fast = head;

  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow === fast) return true;
  }
  return false;
}

// Find Middle Node of Linked List
function findMiddle(head) {
  let slow = head;
  let fast = head;

  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
  }
  return slow;
}
```

---

### Binary Search
Works on sorted collections. Time complexity: $O(\log N)$.

```javascript
function binarySearch(arr, target) {
  let left = 0;
  let right = arr.length - 1;

  while (left <= right) {
    const mid = Math.floor(left + (right - left) / 2);

    if (arr[mid] === target) return mid;
    if (arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }

  return -1;
}
```

---

### Sorting Algorithms

#### Merge Sort — $O(N \log N)$ (Divide and Conquer)
```javascript
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
    if (left[i] <= right[j]) {
      result.push(left[i++]);
    } else {
      result.push(right[j++]);
    }
  }

  return [...result, ...left.slice(i), ...right.slice(j)];
}
```

#### Quick Sort — Average $O(N \log N)$, Worst $O(N^2)$
```javascript
function quickSort(arr) {
  if (arr.length <= 1) return arr;

  const pivot = arr[arr.length - 1];
  const left = [];
  const right = [];

  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) left.push(arr[i]);
    else right.push(arr[i]);
  }

  return [...quickSort(left), pivot, ...quickSort(right)];
}
```

---

## 6. Advanced Algorithmic Techniques

### Recursion & Backtracking
Recursion solves problems by breaking them into smaller subproblems. Backtracking explores all possibilities and undoes choices that lead to dead ends.

```javascript
// Generate all permutations of a string (Backtracking)
function permute(str, prefix = '') {
  if (str.length === 0) {
    console.log(prefix);
    return;
  }
  for (let i = 0; i < str.length; i++) {
    const remaining = str.slice(0, i) + str.slice(i + 1);
    permute(remaining, prefix + str[i]);
  }
}

// N-Queens problem (Backtracking)
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

### Dynamic Programming (DP)
DP solves complex problems by breaking them into overlapping subproblems and storing results to avoid redundant computation.

```javascript
// Fibonacci with Memoization (Top-Down)
function fib(n, memo = {}) {
  if (n in memo) return memo[n];
  if (n <= 1) return n;
  memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
  return memo[n];
}

// 0/1 Knapsack Problem
function knapsack(weights, values, capacity) {
  const n = weights.length;
  const dp = Array.from({ length: n + 1 }, () => Array(capacity + 1).fill(0));

  for (let i = 1; i <= n; i++) {
    for (let w = 0; w <= capacity; w++) {
      if (weights[i - 1] <= w) {
        dp[i][w] = Math.max(
          dp[i - 1][w],
          dp[i - 1][w - weights[i - 1]] + values[i - 1]
        );
      } else {
        dp[i][w] = dp[i - 1][w];
      }
    }
  }
  return dp[n][capacity];
}

// Longest Common Subsequence (LCS)
function longestCommonSubsequence(text1, text2) {
  const m = text1.length;
  const n = text2.length;
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

### Greedy Algorithms
Greedy algorithms make the locally optimal choice at each step, hoping to find a global optimum.

```javascript
// Activity Selection Problem
function activitySelection(start, end) {
  const activities = start.map((s, i) => [s, end[i]]);
  activities.sort((a, b) => a[1] - b[1]);

  const selected = [activities[0]];
  let lastEnd = activities[0][1];

  for (let i = 1; i < activities.length; i++) {
    if (activities[i][0] >= lastEnd) {
      selected.push(activities[i]);
      lastEnd = activities[i][1];
    }
  }
  return selected;
}

// Coin Change (Greedy - works with canonical coin systems)
function coinChangeGreedy(coins, amount) {
  coins.sort((a, b) => b - a);
  const result = [];
  let remaining = amount;

  for (const coin of coins) {
    while (remaining >= coin) {
      result.push(coin);
      remaining -= coin;
    }
  }
  return remaining === 0 ? result : null;
}

// Fractional Knapsack
function fractionalKnapsack(items, capacity) {
  // items: [{weight, value}]
  items.sort((a, b) => (b.value / b.weight) - (a.value / a.weight));

  let totalValue = 0;
  for (const item of items) {
    if (capacity <= 0) break;
    const take = Math.min(item.weight, capacity);
    totalValue += (item.value / item.weight) * take;
    capacity -= take;
  }
  return totalValue;
}
```

---

### Graph Algorithms (BFS, DFS, Dijkstra)

```javascript
// Dijkstra's Shortest Path Algorithm
class WeightedGraph {
  constructor() {
    this.adjacencyList = new Map();
  }

  addVertex(vertex) {
    if (!this.adjacencyList.has(vertex)) {
      this.adjacencyList.set(vertex, []);
    }
  }

  addEdge(v1, v2, weight) {
    this.adjacencyList.get(v1).push({ node: v2, weight });
    this.adjacencyList.get(v2).push({ node: v1, weight });
  }

  dijkstra(start) {
    const distances = {};
    const priorityQueue = new PriorityQueue((a, b) => a.priority - b.priority);
    const previous = {};

    for (const vertex of this.adjacencyList.keys()) {
      distances[vertex] = Infinity;
      previous[vertex] = null;
    }
    distances[start] = 0;
    priorityQueue.push({ vertex: start, priority: 0 });

    while (!priorityQueue.isEmpty()) {
      const { vertex: current } = priorityQueue.pop();

      for (const neighbor of this.adjacencyList.get(current)) {
        const distance = distances[current] + neighbor.weight;
        if (distance < distances[neighbor.node]) {
          distances[neighbor.node] = distance;
          previous[neighbor.node] = current;
          priorityQueue.push({ vertex: neighbor.node, priority: distance });
        }
      }
    }
    return { distances, previous };
  }
}
```
