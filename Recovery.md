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