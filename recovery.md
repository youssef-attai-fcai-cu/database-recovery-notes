# Recovery

## Steal

Transaction made changes that can be flushed before it commits.

Dirty bit: 1
Pin-unpin: 0

## No-Steal

Transaction made changes that can NOT be flushed BEFORE it commits, but can be flushed AFTER it commits.

Dirty bit: 1
pin-unpin: 1

## Force

Flush changes as soons as they are made.

If a transaction reached its commit, then it definetly flushed all its changes.

## No-Force

No pressure, flush AFTER commit. Changes do not have to be flushed before the transaction commits.

## Checkpoint

Flush all changes before checkpoint that have dirty bit = 1 and pin-unpin = 0.

Transactions that have committed before the checkpoint are not of any concern to recovery techniques.

## Deferred Update (No-Undo/Redo)

No changes are flushed before the transaction commits.

Any transaction that still hadn't committed has no affect on the database.

Defer flushing until commit. (No-Steal + No-Force)

At checkpoint, flush changes of only the committed transactions.

## Immediate Update

Any change is immediatly flushed.

### Undo/No-Redo (Steal + Force)

### Undo/Redo (Steal + No-Force)

# PRACTICALY VS. THEORITICALLY

Practically: Flush changes after commit EVEN BEFORE checkpoint

Theoritically: Flush changes after commit AND ONLY AFTER checkpoint