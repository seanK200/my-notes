# 17. Transactions

## Issues to address

- Failures
- Concurrent execution

## ACID

- `Atomicity`: Either all or none
- `Consistency`: Preserved by isolation
- `Isolation`: Unaware of other transactions
- `Durability`: After completion, changes persist despite failures

## Transaction States

1. `ACTIVE`
1. `PARITALLY COMMITTED`
1. `FAILED`: onError
1. `ABORTED`: After rollback
1. `COMMITTED`

## Implementing Atomicity and Durability

Recovery-management component

### Shadow Databse Scheme

Inefficient

## Concurrent Execution

### PROS

1. Increased processor/disk utilization
1. Reduced response time

### Control Schemes

- Achieve **isolation**
- Keep **consistency**

## Schedules

Chronological order in which instructions of concurrent transactions are executed

### Rules

- _All_ instructions need to be run
- _Order_ of individual transaction needs to be preserved

### Serializability

- Serial schedule
- Serializable: Equivalent to a serial schedule
  - Conflict serializable
  - View serializable

### Conflict Serializability

A _conflict serializable_ schedule is _conflict equivalent_ to a serial schedule.

#### Conflict

A conflict enforces **temporal order** between instructions. Instructions $I_i$ and $I_j$ are conflicting *iff*...

- For some item $Q$, instructions $I_i$ and $I_j$ (each of transactions $T_i$ and $T_j$)
- both accesses $Q$, and
- at least one wrote $Q$.

#### Conflict Equivalent

Conflict equivalent schedules $S$ and $S'$ can be converted to each other by a series of swaps of _non-conflicting_ instructions

### View Serializability

A _view serializable_ schedule is _view equivalent_ to a serial schedule.

#### View Equivalent

View equivalent schedules $S$ and $S'$ must follow the 3 conditions below:

1. $initread(Q)$
   - `if` transaction $T_i$ reads initial value of $Q$ in schedule $S$,
   - `then` $T_i$ must also read _initial_ value of $Q$ in schedule $S'$
1. $read(Q \larr T_j)$
   - `if` $T_i$ reads $Q$ produced by $T_j$ in $S$,
   - `then` $T_i$ must also read $Q$ produced by $T_j$ in $S'$.
1. $finalwrite(Q)$
   - `if` $T_i$ performs final write of $Q$ in $S$,
   - `then` $T_i$ must also perform _final_ write of $Q$ in $S'$.

### Serializability Test

#### Precedence graph

- Directional Graph
- $V$: Transactions
- $E$: Connects conflicting transactions. Direction indicates data access order (earlier $\rarr$ later)
- Edge Label: Data item with conflict

#### Testing Conflict Serializability

- A schedule is _conflict serializable_ *iff* its **precedence graph** is *acyclic*.
- Topological sorting can yield **serializability order** (for acyclic precedence graphs)

#### Testing View Serializability

- A **NP-complete** problem
- Practical algorithms can check _sufficient_ view serializability
