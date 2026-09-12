# MVCC

mvcc means multi-version concurrency control,

you might think that when a row is updated in postgres, they are changed in the physical location immediately, that makes sense, but what if the row is being read by someone, and they need the old data, so this is very cleverly solved by creating another tuple, and marking the previous one as dead( this is done by two variables called xmax and xmin, they basically tells when this tuple is created and when it got deleted), so the readers will be able to read it, but writer will write it into a new tuple

when a row is deleted, postgres marks the tuple such that it wont be visible for unnecessary transactions

then doesn't that take too much space, and duplicate data and stale data????, yeah you are absolutely right, that is where vacuum comes into picture, vacuum basically cleans the space of the tuples that are no longer needed by any transaction
