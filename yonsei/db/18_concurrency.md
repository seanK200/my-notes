# 18. Concurrency Control
Concurrent access control schemes

## Lock-Based Protocols
A **lock** controls concurrent access to a data item. 

### Lock Modes
#### `EXCLUSIVE(X)` mode
* READ & WRITE
* `lock-X` instruction

#### `SHARED(S)` mode
* READ only
* `lock-S` instruction

### Lock Request
* **Requests** are made to the concurrency-control manager.
* Transaction can proceed only after the request is *GRANTED*.

### Lock Compatibility

|       | $S$       | $X$       |
|---    |---        |---        |
| $S$   | `true`    | `false`   |
| $X$   | `false`   | `false`   |

* If requested lock is **compatible**, lock is *GRANTED*
* If not, *WAIT* until incompatible locks are released
* Follow a **locking protocol**
    * A set of rules to request/release locks
    * Restricts the set of possible schedules

### Two-Phase Locking (2PL) Protocol
Ensures *conflict-serializable* schedules. 

#### PHASE #1: `GROWING` Phase
* Transaction **may** *obtain* locks
* Transaction **may not** *release* locks

#### PHASE #2: `SHRINKING` Phase
* Transaction **may not** *obtain* locks
* Transaction **may** *release* locks

Transactions can be serialized in the order of their **lock points** (provable). A **lock point** is the point where a transaction acquired its final lock. 2PL does **not** ensure **deadlock** prevention.

### Modified 2PL

#### Strict 2PL
* Tranasaction must hold *all exclusive* locks until commit/abort.
* Prevents **cascading rollbacks** (caused by dirty reads)

#### Rigorous 2PL
* Transaction must hold *all* locks until commit/abort.
* Transactions can be serialized in the order they commit.

## Deadlock Handling
A **deadlock** is a cycle of transactions waiting for locks to be released by each other. We deal with deadlocks by:
1. Deadlock **Detection**
1. Deadlock **Prevention**

### Deadlock Detection
#### Wait-for graph
* V: Transactions
* E: $T_i \rarr T_j$  ($T_i$ is waiting for $T_j$)

A system is in a deadlock state *iff* the wait-for graph is *cyclic*. Periodically check for cycles.

#### Recovery
* Choose a victim (to be rolled back): Select tx with minimum rollback cost
* How much to roll back?: Total rollback(X) *vs.* Only as far as necessary to break deadlock(O)
* Prevent starvation: Include # of rollbacks as a cost factor