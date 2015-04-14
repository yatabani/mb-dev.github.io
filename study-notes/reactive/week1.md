---
tags: ['study-notes', 'reactive']
title: 'Principles of Reactive Programming'
---
[https://www.coursera.org/course/reactive](https://www.coursera.org/course/reactive)

# Week 1 - Recap

## What is Reactive Programming?
- Applications that are event driven - react to events, react to load (scalable), react to failures (resilient), react to users (responsive).
- Event-Driven:
  - Use of non-blocking events.
- Scalable:
  - Make use of multi-core systems
  - Make use of multiple server nodes
  - Minimize shared mutable state and location transparency.
- Resilient
  - Can recover from failures - software/hardware/connections.
- Responsive:
  - Built on all the above in order to respond during load

## Callbacks:
- We usually used event handlers for callbacks.
- Problems: event handlers need to have side effects, cannot be composed and leads to callback hell.

## Functions and Pattern Matching:
- How to represent JSON structure using Scala case classes
- pattern matching
- Function1 trait
- Partial Function - isDefined

## Collections
- map, flatMap, filter.
- for expression translation to map, flatMap and filter.

## Generators
- Example: Generating random numbers.
- Testing using random values

## Monads
- objects containing unit and flatMap.
