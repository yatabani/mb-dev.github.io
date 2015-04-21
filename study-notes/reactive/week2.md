---
tags: ['study-notes', 'reactive']
title: 'Principles of Reactive Programming'
---
[https://www.coursera.org/course/reactive](https://www.coursera.org/course/reactive)

# Week 2 - Dealing with state

## Functions and State
- [Church–Rosser theorem][1] applied to functional programming. We can compute any part of a functional program and still get to the same result at the end.
- An object has a state, if it's behavior is influenced by it's history
- Stateless objects that invoke stateful objects, become stateful.

## Identity and Change
- Objects are the same if they are operationally equivalent
- Testing objects for operational equivalence

## Loops
- Loops can be implemented as tail recursive functions.

## Discrete Event Simulation
- Digital Circuits, signals are true/false and the gates are: Inverter, And, Or
- There's also delay until effect takes place.
- Using classes Wire, Gate
- Simulation and how gates are modeled.
- Observer pattern

## Functional reactive programming
- FRP implementation of Signal and Var that monitor changes to underlying data and modify other signals accordingly.
- This is implemented using global state which is not multi-threaded safe
- We can solve it using various methods but they all have disadvantages as well.

**Assignment**: Calculator

[1]:http://en.wikipedia.org/wiki/Church%E2%80%93Rosser_theorem
