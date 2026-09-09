# Index

as i have thought, indexes are a b tree, basically if index is based on number, the root node has a range, 0-10(1st child), 11-20(second child), so on, this size of each child can differ, and there can be many constraints, and then each child subdivides and goes to the leaf node, leaf node is a memory location of that particular tuple, so it does not store the actual table, but the addresses are stored

but if you think for a second indexes can be very costly, because if there is write to the db, and it effects our column which we have indexed, we might have to change the b tree based on the change

there could be partial indexes, lets say something like

create index user_index on users(email) where active = true

so here only the users whose state is active are present in our index
