# ACID

atomicity : either a transaction succeeds or fails, yeah yeah we know that, but what does that even mean, if there are 10 writes to the data base to different tables in a single transaction, all the 10 writes should happen, or none should happen, there should not be a state where only 5 happen and remaining 5 failed, this in the core is just meaning less

consistency : no the cap theorem consistency, every write should have a correctness, what do i mean, so there are some logical values for our columns, it could be ranges, for example inventory should never be less than 0, if a write is happening where the inventory is being written as -1 is invalid, similar to this there could be many other cases

Isolation : if multiple transactions are happening, they will happen concurrently, but the final result should be such that they have ran sequentially

durability : once something is written to db, it should stay even if the db server crashes for some reason
