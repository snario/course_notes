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




