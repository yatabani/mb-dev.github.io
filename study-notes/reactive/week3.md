---
tags: ['study-notes', 'reactive']
title: 'Principles of Reactive Programming'
---
[https://www.coursera.org/course/reactive](https://www.coursera.org/course/reactive)

## Monads and effects (Try)
- Talk about Sync/Async functions that return one vs. many values
- Actions can fail with exceptions. Usual functions don't tell us that they can fail.
- We want to expose in the type that something can go wrong.
- Instead of returning T, we can return Try[T] to express the function can fail
- (Showing definition of Try)
- Code becomes simpler with flatMap even though there are Try[T]. Or for comprehensions


## Latency as an effect (Futures)
- We want to have a way to express the delay between one function call to the next.
- For this we provide Future.
- Using higher order functions.
- Using zip to combine futures
- using recover and recoverWith

## Composing Futures
- retry combinator
- using foldLeft to avoid recursion.
- using Async await
- Promises
