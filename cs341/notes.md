# CS 341

Algorithms.

## Introduction

The general pattern / workflow of this course will be:

```
Problem --> Design Algorithm --> Analyze algorithm --> Program
                  ^      Do better      |
                  |---------------------<
```

We will also go into areas of proving lower bounds / hardness in general for a Problem, and in some cases we will change the Problem.

#### Problem 1

Given `n` numbers `a_1, ..., a_n`, find the minimum. For example,

Input: `8, 9, 14, 3, 7, 5, 2, 11`

Output: `2`

**Algorithm 1**:

```python
1. min = a_1
2. for i = 2 to n do
3.     if a_1 < min then
4.        min = a_1
5. return min
```

**Analysis**:

How fast is it? Time is the # of operations.

line 1 takes `c_1` time for some const `c_1`

line 3 takes `c_3` time for some const `c_3`

line 4 takes `c_4` time for some const `c_4`

lines 2-4 take `(c_3 + c_4)(n-1)` total time

line 5 takes `c_5` time

So the total time is `c_1 + (c_3 + c_4)(n-1)+ c_5 = Θ(n)`

