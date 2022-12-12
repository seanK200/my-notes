# 19. Recovery

## Failure Classification

### Transaction Failure
* Logical errors: Logical error condition
* System errors (e.g. deadlock)

### System Crash
* Hardware (e.g. power), or software failure

### Disk Failure
* Disk failure (e.g. head crash), destroys all/part of storage

## Recovery Algorithms
Recovery algorithms ensure `CONSISTENCY`, `ATOMICITY`, and `DURABILITY`.

1. **During Transactions:** Leave enough information to recover from failures

2. **After Failures**: Recover contents to ensure atomicity, consistency, and durability.

To ensure `ATOMICITY`, 
1. Output information describing modifications to **stable storage** (log record)
1. Modify the database itself.

## Data Access

### Blocks
* Buffer Blocks: Main memory (temporary)
* Physical Blocks: Disk (permanent)

### Work Area
* Transaction $T_i$ has *private* **work area** in *main memory* with local copies of all data items accessed and updated by $T_i$.

### Instructions
---

<div style="text-align: center;">

**Work Area**

`read(B)` $\uarr$ &nbsp; $\darr$ `write(B)`

**Buffer Block**

`input(B)` $\uarr$ &nbsp; $\darr$ `output(B)`

**Physical Blocks**

</div>

---

> No need for $output(B_x)$ to follow $write(B_x)$ immediately

## Log-Based Recovery
Assumptions: `a)` Log records are written directly to **stable storage** without being buffered. `b)`Transactions are run serially.

$redo(T_i)$ sets all data items updated by the transaction to the *new* values.

### Deferred Database Modification

#### During Transaction
Defer all writes until transaction partially commits.

1. $start(T_i)$
1. Write `T_i START` to log
1. $write(X)$
1. Write modifications to the **log**, and *defer* the actual write.
1. $partially\_commit(T_i)$
1. Write `T_i COMMIT` to log
1. Read the log and actually *execute* the deferred writes

#### After crash
1. $redo(T_i)$ in order if both `START` and `COMMIT` is in log.


### Immediate Database Modification

#### During Transaction
* Writes can occur while transaction is still active. 
* $output(B)$ can take place at any time, at a different order from $write(B)$.
* Contains both old *and* new values of items

#### After crash
1. $undo(T_i)$ restores data items to the *old* value, going **backwards** from the *last* log entry
1. $redo(T_i)$ update data items to the *new* value, going **forwards** from the *first* log entry


## Checkpoints
### Problems
* Search of entire log is time-consuming
* Transactions that need redo are actually already written

### Perform checkpints
1. Output all log records (main memory → stable storage)
1. Output all buffered blocks (main memory → stable storage)
1. Output log record to stable storage: `CHECKPOINT`

### During Checkpoint Recovery
1. **Redo** all transactions after checkpoint (transactions that already output to disk)
1. **Undo** all transactions during system failure.

## Write-Ahead Logging (WAL)
Before a block $B_x$ can output to disk, all log records about $x$ needs must be output to stable storage first.