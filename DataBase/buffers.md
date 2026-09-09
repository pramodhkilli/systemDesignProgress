# Shared buffers

shared buffers are kind of like a cache in the postgres world, whenever a read request comes, it first checks if it is present in this shared buffer, if present great, we'll return it, if not, then we go to the page and fetch that data

then what is a WAL, it is write ahead log, so whenever a write request comes, a log is stored, that this data has been changed from x to y, this helps in the case of database outages, it stores all the history of the changes, so there is physical local for where the WAL is stored in the disc, and for that there is a buffer specially for WAL as well, so the log first gets written to the buffer, and eventually written to the physical location

check points : if WAL kept growing forever, recovery could become increasingly expensive, so postgres periodically performs checkpoints. these act as a recovery point if somehow we faced a crash.

what happens in crash recovery : so if some changes are not persisted to the physical location, then when the server starts, it reads the wal records, does any changes required, from a previous checkpoint maybe, and gets the database to a consistent state
