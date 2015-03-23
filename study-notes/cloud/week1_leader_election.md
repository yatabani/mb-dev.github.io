# Week 1 - Leader Election

## Ring Election Leader

Similar to Chord p2p system

N3 -> N32 -> N5 -> N80 -> N6 -> N12 ->

Any process that discovered coordinator failed - initiates an election. And it contains it's own id.

When a process receives a message.
* If the attr is greater than own, Pi forwards it
* If attr is smaller and Pi not forwarded an election, it overwrites the message with it's own id and forwards it
* If the arrived id matches that of Pi, then it menas that Pi is the highest member and so gets elected. Then we send **Elected** message to neighbor to announce election result.

When process $p_{i}$ receives an Elected message, it:
* Sets it's variable $elected_{i}$ to equal the id of the message
* forward the message unless we reached the leader.

Example from above:
* N3 initiates the election.
* 3 -> 32 -> 32 -> 80 -> 80 -> 80 -> (until N80)
* Then 80 is sent around until reaching M80 again

## Analysis
Worse case is if the initiator is the successor of the would be leader.
* N-1 message to get around
* N messages for election
* N messages for elected
* (3N-1) message complexity, completion time.

Best case:
Initiator is the would be leader. That's 2N.

## Multiple initators?
* Each process can remember in the cache the initiator of each Election/Elected message.
* Then suppressing  Election/Elected messages of lower id initiators
* Result is that only highest id initiators complete

## Effect of failure
* Failures can cause messages not to continue in the ring
* Leader election is difficult since it's related to consensus problem.

## Election in Chubby and Zookeeper
* Using consensus to solve this issue - each process propose a value, everyone in the group reach consensus, the value proposer is the leader.

### Chubby
* Chubby is used for locking and writing small configuration files. Has a group of servers with one of them functioning as the leader.
* When there is a need for leader election, potential leader tries to get votes from other servers, each server votes at most for one leader and majority of votes becomes the new leader.
* Read are answers locally from the master.
* Write are sent to quorum servers (using mutual exclusion)
* **Safe**: Since you use quorum, only one leader is selected at a time.
* **Live**: Eventually live. Worse case was 30s.
* After leader election there is a **Master lease** time, which means server will not run elections during this time (typically a few seconds).
* Master lease can be renewed again as long as he gets priority

### Zookeeper
* Zookeeper requires leaders to be elected at all times
* During election each server creates a new id for itself. Gets the highest id from ZK file system and writes the new high id
* Elect highest id as leader
* Each process monitors it's next higher id process.
* If the successor failed, the monitor system becomes the new leader. Otherwise wait for timeout and check successor again
* What if leader fails during election? Zookeeper sends NEW_LEADER to all, each process responds with ACK to at most one leader. Each process respond with ACK. Leader waits for majority ACK then sends COMMIT to all. When COMMIT received process update it's leader variable.
* **Safety**: Guaranteed since it uses quorum.
* **Liveness**: is not guaranteed since it's possible to have 3 leaders get 1/3 of the votes and not reach consensus.

## Bully Algorithm
* All process know other id's
* When process find the leader failed.
  * Highest ID: elects itself and sends coordinator message to all process with lower identifier, complete
  * Otherwise initiates election by sending Election message to higher process. If they timeout, send coordinator to lower ids and become the leader.
  * When receiving message, wait for coordinator message. If did not receive, start a new election run.
  * Process that receives an Election message, replies with OK and starts with it's own leader election.

Example:<br>
- N3, N5, N6 (Detector), N12, N32, N80 (Failed)
- N6 -> Election to N12,N32,N80
- N12,N32 -> OK to N6
- N12 -> Election to N32, N80
- N32 -> Election to N80
- N32 -> OK to N12
- N32 -> Coordinator N32 to N3,N5,N6,N12

If N32 also failed in the middle, N12 and N6 would timeout and N6 will start new election process.

* Timeouts are set based on worst time to complete election. 5 message transmission times:
  * Election from lowest ID in the group, answer from the 2nd highest id, election from the 2nd highest id, timeout for highest id, coordinator from 2nd highest

Analysis:
* Worst Case: O(N^2) election messages
* Best Case: O(N) coordinator messages, 1 message time
* Liveness not guaranteed due to timeouts.

## Mutual Exclusion

### What?
* How to support network lock?
* To support for example two ATM's making deposits and attemping to modify the final balance.
* Also Distributed file system need to lock files and folders
* Partition work using locks
* Chubby / Zookeeper use locks.
* Critical section problem - enter(), accessResource(), exit()

ATM1: Enter(S), deposit money, exit(S)<br>
ATM2: Enter(S), deposit money, exit(S)

On Local machines it can be solved using mutex, semaphore etc.

### Attributes
A solution in distributed system needs to guarantee:
* Safety - One process executes in CS
* Liveness - Every request for CS will be granted eventually
* Ordering (desireable)- Requests are granted in the order they are made
* Bandwidth - how many messages is required to enter? client delay - how long it takes to enter and exit? sync delay: time between one process exit and the other to enter?

### System Model
* Each pair of process has reliable connection (TCP)
* Messages are delivered FIFO
* Process do not fail (There is a variant in literature)

### Central Solution
* Elect a leader
* Leader keeps a queue of process wishing to access critical section. And token that allows others to acces critical section
* enter() - sends request and wait for token
* exit() - send the token back to master
* **Safety:** There is only one token
* **Liveness:** If process exits eventually and no failures, it's guaranteed
* FIFO Ordering
* Bandwidth: 2 messages, 1 to exit. Delay: 2 message latency, Sync Delay: 2 message latency
* Master is one point of failure

### Ring
* Token passes from one process to another on the ring. If a process is not interested, it passes the token around.
* **Safety:** Only one token
* **Liveness:** Token eventually loops around
* Bandwidth: 1 to get the ticket, 1 to pass it, Client Delay: 0 to N, sync delay: between 1 to (N-1)

### Ricart-Agrawala algorithm (1981)
* Uses causality and multicast
* Enter() - multicast to all process, <T, Pi>, T is lamport timestamp
* Wait until all process responded
* REquested are granted in order of causality
* Pi in request is used to break ties

Algorithm
* enter()
  * set state to Wanted
  * Send request
  * Wait until all process send back Reply
  * change state to Held
* On receipt of request <Tj, Pj> at Pi (i!=j)
  * if (state = Held) or (state = Wanted and <Ti,i> < <Tj,j>) then add requests to local queue
  * else send Reply to Pj
* exit() at process Pi
  * change state to Released and REply to all queued requests.

Example:
- N32 -> <102,32> to *
- N3,N12,N6,N80,N5 -> Reply to N32
- ; N32 state is now held and can enter critical section
- N12 -> <115,12> to *
- ; N12 State wanted
- N80 -> <110, 80> to *
- ; N80 State wanted
- N3,N6,N5 -> Reply to N12
- N3,N6,N5 -> Reply to N80
- N32 queues requests <115,12>, <110,80>
- N80 queues the request <115,12>
- N12 -> Reply to N80 (since id is lower)
- N32 release critical section. -> Reply to N12,N80
- N80 release critical section -> reply to N3

Analysis:
* **Safety:** Two process cannot both have access
* **Liveness:** Worse case wait for other N-1 process to reply
* **Ordering:** By lamport timestamps
* Bandwidth: Client sync delay is now down to O(1) but bandwidth is O(N)

### Maekawa's Algorithm (1987)

- How about we require reply from only some processes?
- Each process Pi is associated with a voting set Vi (of processes), each voting set is a quorum.
- Each voting set is size K, each process belongs to M other voting sets. K=M=sqrt(N) works best.
- if we have four process in the system:
![Voting Sets](./VotingSets.png)
- Each process requests permission from only it's voting set members. Each process gives permission to at most one process at a time.

Actions:
- state = Released, voted = false
- enter() at process Pi  
  - multicast Request to all process in Vi
  - wait for Reply from all process in Vi
  - Set state = Held
- exit() at process Pi - state = Released, send Release to all process in Vi
- when Pi receives a request from Pj
  - if state == Held OR voted = true, queue
  - else send Reply to Pj and set voted = true
- when Pi receives a release from Pj
  - if queue is empty then voted = false
  - else dequeue head of queue, Pk, send reply only to Pk, voted = true

Analysis:
- **Liveness:** Can result in deadlock. (There are deadlock free versions)
- Bandwidth: 2sqrt(N) per enter(), sqrt(N) per exit().
- Client delay: One round trip, sync: 2 message time.
