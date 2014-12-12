# CS 240 Review

## Introduction and Asymptotic Analysis

Mostly definitions and proving order functions.

## Analysis of Algorithms

There are different types:

### Linear algorithms

Easy to write summations for them. Just need to simplify the expression.

### Recursive algorithms

Write the recursion equation and solve for the correct term.

## Abstract Data Types

### Stack

A list of items that runs FIFO.

### Queue

A list of items that runs LIFO.

### Priority Queue

- Like a queue but order is not based on time of insertion; based on value of key.
- Can be implemented using **heaps**. A heap has the heap property which is that every nodes children are less or more than the node.
- With heaps for any deletion you move the bottom-right element to where the deleted element was and then you *bubble-down*.
- For any insertion, you add to the bottom right and bubble up.

## Sorting

### Priority Queue Sort

Put everything into a priority queue and then deleteMax. O(n lg n)

### Heap Sort

Speciailization of Priority Queue sort. Insert all the elements using `heapify`

### Quick Sort

To begin, think about something called Quick Select. Finding the k-largest element.

**Worst-Case** each recursive call has size `n - 1` leading to `O(n^2)` time.

**Best-Case** 0 recursive calls, `O(n)`.

**Average-Case** `O(n)`

Now for Quick Sort, it is basically just the same as Quick Select but you take both paths.

**Worst-Case** each recursive call has size `n - 1` leading to `O(n^2)` time.

**Best-Case** 0 recursive calls, `O(nlogn)`.

**Average-Case** `O(nlogn)`

### Lower Bounds for Sorting

If we use The Comparison Model, we can prove there is an Ω(n log n) lower bound on sorting. None comparison sorts are different.

### Counting Sort

Does not use comparison. Essentially just loads a new array C of length max(A) where C[i] = count(A, i). E.g., [1 5 2 4 5] --> [0 1 1 0 1 2] then reduces this like [0 1 2 2 3 5], then A[--C[B[i]]] = B[i].

Time: O(n)
Space: O(n + k)
Stable!

### Radix Sort

Counting sort on single digits of numbers from the end to the front for each digit. Works best on lists of equal length numbers.

Time: Θ(d(n + k))
Space: Θ(n + k)

### Summary

- Randomized algorithms can eliminate “bad cases”
- Best-case, worst-case, average-case, expected-case can all differ
- Sorting is an important and very well-studied algorithm
- Can be done in Θ(n log n) time; faster is not possible for general input
- HeapSort is the only fast algorithm we have seen with O(1) auxiliary space.
- QuickSort is often the fastest in practice
- MergeSort is also Θ(nlogn), selection & insertion sorts are Θ(n^2)
- CountingSort, RadixSort can achieve o(n log n) if the input is special

## Dictionaries

Collection of items with a key and some data. Search, insert, delete.

### Binary Search Trees

Everything is less on left, more on right.

Everything is Θ(h), but depending on structure can be at worst Θ(n) and best Θ(log n).

### AVL Trees

Same as Binary Search Tree but _balance_ is -1, 0, or 1 all the time (always balanced). There is a _fix_ algorithm that you can run on a tree with balances -2, or 2.

Same analysis as BST but worst case is logarithmic.

### 2-3 Trees

Nodes can have two elements, and three children.
Inserting goes to a leaf and if necessary splits it and floats upwards until happy.
Deletion first swaps with the successor, then deletes if it is a 2-node. If it is a 1-node then either it has a 1-node neighbour or it doesn't. If it has a 1-node neigbour, put the parent in the neighbour and recursively delete upwards. Otherwise reshuffle.

### B-trees

A B-tree of minsize d is a search tree satisfying that:
- Each nodes has at most 2d KVPs, each non-root node contains at least d KVPs.
- All leaves are at the same level.

A 2-3 tree is a B-tree of order (2d + 1) with d = 1 (or a (d + 1, 2d+ 1))-tree.

## Hashing

### Direct Addressing

This just means instant lookup like you expect. We can make hash functions, but the hard part is dealing with collisions.
There are two common methods: _division method_ (k mod M) and _multiplication method_ (floor(M(kA - floor(kA)))).
There are a few strategies. Don't forget *load balance* is alpha = n/M. n is number of elements, M is size of dictionary.

### Chaining

Each entry is a bucket. We have Θ(1 + alpha) average case search, Θ(n) worst case. Insert is O(1). Delete is same as search.

### Open Addressing

Every hash table entry has *only one item*. We follow a probe sequence of hashing functions. Means we need to differentiate between empty and deleted.

Example: h(k, i) = (h(k) + i) mod M

## Double Hashing

Define h(k, i) = h1(k) + i*h2(k) mod M and use linear probing with this thing.

### Cuckoo Hashing

The whole point of this is to get O(1) inserting.

We use h1(k) to try to insert, if it is empty then great. Otherwise we put it in anyway and re-insert the item that was there with the other hash function.

### Extensible Hashing

There is a hashtable directory. Each entry is a d length binary string.

Each entry points to a block of max length S.

Each block's elements agree with the first d bits of its corresponding entry in the directory.

You just need to work through some examples to understand this.

### Summary

*Advantages of Balanced Search Trees*
- O(log n) worst-case operation cost
- Does not require any assumptions, special functions, or known properties of input distribution No wasted space
- Never need to rebuild the entire structure

*Advantages of Hash Tables*
- O(1) cost, but only on average
- Flexible load factor parameters
- Cuckoo hashing achieves O(1) worst-case for search & delete

*External memory*
-Both approaches can be adopted to minimize page faults.

## Dictionary Tricks

### Interpolation Search

This is just binary search with some flair. If the keys are uniformly distributed then we get O(log log n) on average. Worst case is O(n) though.

Instead of `l + floor((r - l)/2)` we do `l + floor([(k - A[l]) / (A[r] - A[l])]*(r - l))`

### Gallop Search

Good for if we don't know where the end of the array is. O(log m) comparisons (m is the location of k in A).

### Self-Organizing Search

Sort items by probability of being accessed.

### Dynamic Ordering

When you access an item, either move it to the front or move it up one in line.

### Skip Lists

Every insert you roll a dice for k heads until the first tail and k determines the height of the tower.
When traversing in a search you start at the topleft and go as far as you can, then drop down, and repeat.
Insert is just search until you find the largest item less than the new one and place it before it.

Space is O(n). Height is O(log n). O(log n) expected everything else.

## Multi-Dimensional Data

All the data is in euclidean n-space. We usually talk about 2-space.

### 1-D Range Search

Using an AVL tree as the base, we make a tree on one dimension.
There is a notion of boundary, inside, or outside when searching a range.
Not every boundary node is returned. For 1-D we get O(log n + k) where n is all nodes, k is the inside nodes.

### 2-D Range Search

Each node corresponds to 2 coordinates.

### Quadtrees

All about subdiving a square plane R into quadrants recursively.

Using Quadtrees for range searches is wasteful on space, easy to compute, not complicated, can easily have large height for nonuniform data. Easily generalizable.

Height is Θ(log dmax / dmin). Worst-case initial build is Θ(nh). Range search is also Θ(nh) worst case.

### kd-trees

Split into two at the median and alternate the axis each time you split.

Complexity is Θ(n log n), height is Θ(log n).

Range query time is O(n^(1-1/d) + k)

### Range trees

Tree of trees. Each node points to a new tree of the next coordinate of the children of the original node.

Search is trivial.
Insert adds to tree and then you walk up adding to all parents.
Rebalancing is a problem.

1. Do a BST range search
2. For every outside node, skip. For every _top inside_ node, do a range search on the y interval. For every boundary node, test if inside R.

Running time is O(k +log^2(n)). Construction is O(n logn). Space is O(n logn).

## Tries and String Matching

### Tries

Dictionary for binary trees. Left is 0 right is 1, height is index of string. One caveat: they are _prefix-free_.

prefix-free: no key is a prefix of another key

### Multiway Tries

Same as tries but abstracted over an alphabet. However we need to append an end-of-word character as a leaf when a word is present.
Compression is the same, just add nodes for indicies.

T of length n is the text.
P of length m is the pattern.

### Algorithms

A guess is a start position i so P _might_ start at T[i].
A check of a guess is a position j < m where we compare T[i+j] to P[j].
**KMP** is an algorithm which does some preprocessing on P and eliminates bad guesses.

Basically with KMP we find the largest prefix of P[0..j] that is a suffix of P[1..j]. F[j] is the length of that.

*Boyer-Moore* is an algorithm that
1. compares backwards
2. jumps bad characters
3. finds good suffix jumps

To compute the suffix array, start with the last character. What you do is find the index of the last character that is NOT the character you're on now, followed by the characters that follow it.

It's usually better than KMP on English text. At worst runs in O(n + |Alphabet|)

### Suffies Trees (Suffix Tries)

Useful for searching for many patterns not just one. We preprocess T not P. P is a substring iff P is a prefix of a suffix of T.

- build a compressed trie for all suffixes of T
- insert suffixes in decreasing order of length
- don't include prefixes of other suffixes
- store indices at each node representing beginning and ending of substring in T (l and r)

### Summary of Pattern Matching

Brute Force vs KMP vs Boyer-Moore vs Suffix Trees

Preprocessing = ---, O(m), O(m + |Σ|), O(n^2)

Search Time = O(nm), O(n), O(n), O(m)

Extra Space = ---, O(m), O(m + |Σ|), O(n)

## Compressions

S is source, C is coded.

### Run-Length Encoding

Variable length code, fixed decoding dictionary, not explicitly stored.

- encoding of run-length k must be prefix-free
- put first 1 or 0 at beginning
- changes runs of length k to floor(log(k)) 0's concatenated with k in binary

### Huffman Coding

Build a binary trie to store the decoding dictionary D. Each char is a leaf of the trie.

The hard part is building the trie, we need to:

- determine frequency of every char c in Σ in S.
- make |Σ| tries with just the one character c in Σ. assign a weight to each one (char frequency, but really is sum of all chars just 1 to start)
- merge the two worst together and repeat

Best to use a min-heap to store each trie.
**Summary**

Encoder does lots of work (O(|S| + |Σ|log|Σ|) building decoding trie)

The constructed trie is not necessarily unique.

*Huffman is the best we can do for encoding one character at a time*.

### Move-to-Front

Example of an adaptive dictionary.

For every char in S we move the char in the dictionary (linked list) to the front. After that we encode the int sequence from encoding.

### Lempel-Ziv

Each character in the coded text C either refers to a single character in ΣS , or a substring of S that both encoder and decoder have already seen.

Basically as we add, we take the last subtring and first char in the next substring and add it to dict after looking up the current substring.

### Burrows-Wheeler Transform
**Encoding** O(n^2) using radix sort (needs to be stable!)

1. Place all cyclic shifts of S in a list L
2. Sort them lexicographically
3. Extract the last characters from the sorted shifts

C = result from 3
**Decoding** O(n)

1. Make array of A of tuples (C[i], i)
2. Sort A by the characters, record integers in array N
3. Set j to index of $ in C and S to empty string
4. Set j = n[j] and append C[j] to S
5. Repeat step 4 until C[j] = $

### Summary

- **RLE** Variable-width, multiple-character encoding
- **Huffman** Variable-width, single-character (optimal in this case)
- **MTF** Adaptive, transforms to smaller integers, must be followed by variable-width integer encoding
- **LZW** Adaptive, fixed-width, multiple-character encoding Augments dictionary with repeated substrings
- **BWT** Block compression method, must be followed by MTF
