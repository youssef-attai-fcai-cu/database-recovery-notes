# Recovery

## Concepts

### **Dirty bit**

A boolean flag associated with every block coming from the hard disk to the main memory for a transaction to process it.

If the value of the dirty bit is **0**, then the buffer is unmodified, and the transaction only read the data items it needed from the block.

If the value of the dirty bit is **1**, then the buffer is modififed by the transaction.

### **Pin-unpin bit**

A boolean flag that describes whether a block in the main memory can be flushed to the hard disk.

If it's value is **0**, then the buffer can be flushed, if it is **1**, then it can not be flushed.

#### _Steal/No Steal: Can you write?_

#### _Force/No Force: When to write?_

### **Steal** (yes, you can write)

A data block in the main memory is modified, and can be flushed to the hard disk BEFORE the transaction commits.

Dirty bit = 1 (modified buffer)
Pin bit = 0 (can be flushed)

### **No Steal** (No, you can not write)

A data block in the main memory is modified, but can NOT be flushed to the hard disk until AFTER the transaction commits.

### **Force** (DO IT RIGHT NOW)

Any change by a transaction should be flushed, so that when a transaction reaches it's commit, all changes it made are already flushed to the hard disk.

### **No Force** (Do it at any time)

Any change by a transaction can be flushed at any time. No pressure.

## Defered Update (No Steal/No Force)

No updates are flushed to the hard disk before the transaction commits before a checkpoint.

For a transaction to be flushed, it has to be _**commited before a checkpoint**_, after the checkpoint, if it was commited, then it is flushed to hard disk.

Any transaction that is not commited, has no effect on the database.

All commited transactions before system crash and after the last checkpoint are **Redone**.

All commited transactions before the last checkpoint are **Ignored**.

All non-commited transactions that are interrupted by system crash are **Restarted**.


**No Roll back (No Undo).**

All updates are flushed after the transaction commits.

If a failure happens after the commit and updates are not yet flushed, then the transaction **Rolls forward (Redo)**.

Practically, flushing happens directly after the transaction commits (doesn't wait for checkpoint).

Theoretically, flushing happens after the transaction commits and the checkpoint.

At the checkpoints, the dirty bit for the modified buffers are = 1, and the pin bit = 0.



## Immediate Update

### Undo/No Redo (Steal/Force)

Any update should be immediately flushed to the hard disk.

All commited transactions are **Ignored**, because they are already flushed.

All interrupted transactions due to system crash are **Undone**, because they flushed some writes but not all.


### Undo/Redo (Steal/No Force)

Any update can be flushed to the hard disk at any time.

All commited transactions are **Redone**.

All interrupted transactions due to system crash are **Undone**, because they flushed some writes but not all.
