---
tags: ['study-notes', 'reactive']
title: 'Principles of Reactive Programming'
---
[https://www.coursera.org/course/reactive](https://www.coursera.org/course/reactive)

## Actors
- Traditional synchronization mechanism such as locks can lead to poor cpu utilization and introduce dead locks.
- Actors solve this by allowing to async send and receive values and streamline behind the scenes.
- Actors can use *become* to simulate tail recursive state change.
- Actors can send messages and addresses of other actors. Messages are processed sequentially.
- Supports three delivery guarantees: at-most-once, at-least-once, exactly-once
- Do not access actor state from code running async and also pipe all futures onto self.

## Failure handling
- Failures in actors is handled by supervision trees. Parents can decide what to do with failing actors.
- AllForOneStrategy - all child actors perform the same recover actions at the same time. I.e. they all restart.
- OneForOneStrategy can accept parameters - maxNrOfRestarts - after that they turn into a Stop.

## Lifecycle
- Actor lifecycle - Start (preStart). Restart (preRestart, postRestart) and postStop handlers.
- Deathwatch allows monitoring actor state.
- Since restarts are costly we can perform safer tasks at the upper layers of supervision tree and delegate riskier tasks to the bottom. This way failure is localized as much as possible.
- EventStream allows broadcasting events to multiple actors.
- Watching another actor and not handling Failure event means the watching actor will be terminated if the watched actor terminates. (DeathPact)

## Persistent Actor State
- Allows not to lose state due to system failure.
- Possible to use snapshot or immutable append log with snapshots.
- persist vs. persist async control whether the actor will keep processing messages while we wait for events to persist.
