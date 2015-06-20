---
tags: ['study-notes', 'reactive']
title: 'Principles of Reactive Programming'
---
[https://www.coursera.org/course/reactive](https://www.coursera.org/course/reactive)

## Distributed Actors
- Actors were written with distributed computing in mind. Actors work locally as though they are distributed.
- Actor path points to where the actor reside.
- ActorRef is the same as ActorPath with added pid.
- Identify allows finding ActorRef from path
- Actor Clusters implement membership protocol and information is passed using gossip protocol.

## Eventual Consistency
- Eventual consistency can be implemented using set of actors that get updates for values using (value, timestamp). Last change will win in case of conflicts.
