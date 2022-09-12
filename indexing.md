# Indexing

The smallest unit of data transfer is a block/page.

A block/page contains multiple records.

## Index

An index is a sorted auxilary structure, it helps in searching for data items in
a table by opening the door to binary searching.

An index can be either **dense** or **sparse**

### Dense index

A dense index has an entry for every search key in the indexed table file.

e.g.

Key | Reference |
--- | ---       |
A   | 1         | 
B   | 2         | 
C   | 3         |

RRN | Key | Data |
--- | --- | ---  |
1   |  A  | foo  |
2   |  B  | bar  |
3   |  C  | baz  |

### Sparse index

A spare index is non-dense, which means not all search keys are going to have an
index entry in a sparse index.

e.g.

Key | Reference |
--- | ---       |
A   | 1         |
C   | 3         |

RRN | Key | Data |
--- | --- | ---  |
1   |  A  | foo  |
2   |  B  | bar  |
3   |  C  | baz  |

A sparse index can be used when the records are sorted on the search key in the
data file.

Usually, since the smallest unit is block and not a record, a sparse index will
have an entry for one key per block.

## Types of indexes

- Primary - Clustering - Secondary - B-Tree or B+Tree

### Primary index

Can be dense or sparse.

### Clustering index

For sequential data files

The keys can be non-unique, but they can NOT be null.

It has an index entry for each distinct key.

### Secondary index

Can be used anywhere with anything.

Secondary indexes must be dense,
with an index entry for every search-key value,
and a pointer to every record in the file.

The field in the data file on which the secondary index
is made is not necessarily ordered.

A primary index is more efficient than a secondary index.

- A primary index is usually sparse
- A clustering index is usually sparse
- A secondary index must be dense