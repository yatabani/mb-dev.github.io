---
tags: ['study-notes', 'algorithms']
title: 'Algorithms'
---
[https://www.coursera.org/course/algs4partI](https://www.coursera.org/course/algs4partI)

## Week 2 - Stacks, Queues, Sorts

### Stacks
- LIFO
- Implemented using Linked list.
- New nodes are inserted to the beginning of the linked list.
- Performance: All operations O(1). Memory: ~40N bytes.
- Another implementation is an array
- Cons: Capacity cannot easily change

### Resizing array
- Increasing and decreasing array capacity with every pop/push is unacceptable
- One technique: doubling. When array is full, create previous-size*2 array.
- Cost inserting first items ~3N
- Shrinking array by the same mechanism has a pitfall - push/pop repeatedly can cause the array to be resized repeatedly.
- Solution: resize by half when the array is a quarter full
- As a result: Linked list based on array has less wasted space but constant **amortized** time

### Queues
- FIFO
- Linked list implementation - add nodes to the end of the list.
- Array implementation - Maintain two pointers, head and tail. enqueue items on the tail, dequeue removes from head.

### Generics
- Use Generics with data structures to allow them to be used with any type.
- Java Generics do not allow declaring generic array. So declare Object[] and cast to the generic type.

### Iterators
- Iterable has method that returns iterator
- Iterator has hasNext() and next()
