---
tags: ['study-notes', 'algorithms']
title: 'Algorithms'
---
[https://www.coursera.org/course/algs4partI](https://www.coursera.org/course/algs4partI)

## Week 1 - Steps to develop an Algorithm
![Imgur](http://i.imgur.com/8TwMfRE.png)

## Week 1 - Union Find
- Network connectivity. Set of N objects with commands: Union and Connected.
- Data Structure #1 (Eager):
  - Array where id[i] starts as equal to i.
  - Connected components get the same id in the array.
  - To connect p-q: (entire array where id[p] == id[q]) set to id[q]
  - Performance: Initialize: N, Union: N, Find: 1
- Data Structure #2 (Quick Union):
  - Array represents a tree.
  - id[i] points to the parent. id[i] = i if it's the root.
  - Union p-q: i=root(p), j = root(q), id[i] = j
  - Performance: Initialize: N, Union: N, Find: N
- Data Structure #3 (Weighted Quick Union)
  - Keep track of size of trees
  - Union: Smaller trees go to the root of the big tree.
  - if size[i] < size[j] id[i] = id[j], sz[j] += sz[i]
  - else                 id[j] = id[i], sz[i] += sz[j]
  - Performance: Initialize: N, Union: lg(n), Connected: lg(n)
  - Improvement by Path Compression: Every time we find the root of a node, connect it directly to the root.
- Applications:
  - Minimum Spanning Trees.
  - Percolation - Is there conductivity in a material?

## Week 1 - Analysis Of Algorithms
- The challenge: will my program be able to give solution for a large input? why does it run out of memory?

### Observations
- Example: 3-Sum - Given N distinct integers. How many triples sum to exactly zero?
- Brute Force: N^3.
- Log log plot - when getting a straight line with slope b, the running time is a*N^b
- Quick way to estimate b in a power-law relationship: Run the program, doubling the size of the input. The ratio will converge to a constant
- After finding b, we can run the program with a specific input size to find a.

### Mathmatical Models
- Total running time - sum of cost x frequency of operations.
- Instead of counting every operation, we can simplify:
- 1) Count only the most expensive operations
- 2) Use tilde ~ notation and ignore lower order terms.

### Order of growth classifications
- Best Case, Worse Case, Average Case
- Theta, Big O, Big Omega

### Memory
- Typical memory usage for types (picture)
