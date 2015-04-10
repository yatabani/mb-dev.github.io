---
tags: ['study-notes', 'cloud']
title: 'Cloud Computing Concepts'
---
[https://www.coursera.org/course/cloudcomputing2](https://www.coursera.org/course/cloudcomputing2)

# Week 3 - Stream Processing &amp; Distributed File System

### Stream process with Storm
- Today's workloads have large amount of data. => need real time view of data
  - Twitter real time search
  - Website statistics
  - Intrusion detection system
- Process large amount of data
  - With low latency and high throughput


- Storm components
  - Tuples - ordered list of elements
  - Spout - source of tuples.
  - Bolt - processes the stream - generates output stream.
  - Topology - graph of spouts and bolts


- Bolts: there are built in bolts:
  - Filter - forward only if justify condition
  - Joins - output pairs, A/B
  - Apply/Transform - modify each tuple


- Grouping of tasks:
  - Round robin
  - Group by fields

### Distributed graph processing
- A graph has network with vertices/nodes
- A graph has edges that connect pair of vertices
- Some algorithms are: Find short path, degree of separation.
- The challenge is that graphs are very large. Hard to store the entire graph on the server and process it.
