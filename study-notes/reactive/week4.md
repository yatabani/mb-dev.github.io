---
tags: ['study-notes', 'reactive']
title: 'Principles of Reactive Programming'
---
[https://www.coursera.org/course/reactive](https://www.coursera.org/course/reactive)

## Observables
- Category theory discussion about turning Future to Try and Iterable to Observable
- Iterable to read files from disk can be slow since next/hasNext are blocking.
- Observable accepts three functions: onNext, onError, onCompleted

## RX Operators
- flatMap on Observables maps each item to async values. As a result merged stream can be out of order
- concat on the other hand will merge the streams in order but we lose the streaming ability.
- groupBy

## More Rx
- Hot vs. cold streams - hot stream - stream is shared and subscription does not matter.
- Multiple subscription classes.
- Subjects - like Promises but for Observables.
- PublishSubject - simple pipe, ReplySubject - has history, BehaviorSubject - returns last value (Subjects are not recommended)
- Observables and Notification
- Observables.toBlocking
- Possible to add [back pressure][1]
- Other implementations [RxJs][2]


[1]: https://github.com/ReactiveX/RxJava/wiki/Backpressure
[2]: https://github.com/Reactive-Extensions/RxJS
