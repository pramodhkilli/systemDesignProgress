# example flow

lets say our springboot application requires a user with the id 42

then client -> postgres backend -> parser -> analyzer -> planner -> index scan selected -> b-tree root page -> internal to leaf page -> tuple address -> tuple -> mvcc visibility check -> name -> executor -> client
