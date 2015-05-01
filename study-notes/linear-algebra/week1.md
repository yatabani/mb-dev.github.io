---
tags: ['study-notes', 'linear-algebra']
title: 'Linear Algebra'
---
[http://ocw.mit.edu/courses/mathematics/18-06sc-linear-algebra-fall-2011/](http://ocw.mit.edu/courses/mathematics/18-06sc-linear-algebra-fall-2011/) [Book - Amazon](http://www.amazon.com/gp/product/0980232716/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=0980232716&linkCode=as2&tag=moshberg-20&linkId=WQOBVOWUE4LMKX3Q)

## 1. The geometry of linear equations (1.1-2.1)

- How to solve n equations with n unknowns.
- Ax = b, A - coefficient matrix, x - unknown vector, b - the result.
- Linear combination of columns.
- Row picture: In 3d - each equation is a plane. Two of them meet in a line, three of them meet at a point.
- Column picture: Draw all vectors as columns.
- Solve Ax = b for every b.
- Multiply matrix by a vector by columns
- Multiply matrix by a vector by rows.

Problem Sets: 1.2: 23, 28. 1.3: 4, 13. 2.1: 29, 30

## 2. Overview of key ideas (1.3)

- Independent vs. dependent vectors
- The basis (Set of independent vectors from which you get the whole space)
- Subspace is a vector space inside a bigger one. Like a plane in R^3 space
- Example of subspaces of R^3: Whole space, plane, line, the origin point (0 dimensions)

Problem Sets: Recitation quiz

## 2. Elimination with matrices (2.2-2.3)
- solving 3 unknowns by elimination
- failure if there's zero in the pivot - use row exchange
- failure because 0=0 (infinite answers),
  or 0!=0 (no answer, parallel lines)
- identity matrix
- using matrix to express elimination
- permutation matrix - exchange rows - multiply on the left.
- permutation matrix - exchange columns - multiply on the right.
- Inverse of matrix - matrix that gives identity

Problem Sets: 2.2: 20, 32. 2.3: 22, 29.

## 3. Multiplication and Inverse Matrices (2.4-2.5)
- Four ways of thinking about matrix multiplication:
- row * columns: $$ C_{34} = A_{31}B_{14} ... = \sum_{k=1}^n a_{3k}b_{k4} $$
- Multiply matrix A by every column in B - to get every column in C
- Every column AB is a combination of columns of A
- Multiplying every row in A with matrix B - linear combination of rows
- Column of A * row of B - sum(columns of A)*(rows of B)
- Block multiplication
- Invertible and non-invertible matrices.
- Gauss Jordan Elimination
