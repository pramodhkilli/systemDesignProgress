# Idempotency

what is idempotency : we call an api idempotent if it process the request such that if duplicate requests comes in, it wont effect the correctness

example : if there is a payment system, and client has made a payment, but somehow due to timeout or duplicate requests, two api calls were made, what is the supposed behaviour??? the payment should be made only once, but here it will be done twice

how do we handle such cases??? we use a key, in each request we send a UUID(universally unique identifier), so in the above case the two requests will have the same id, so when server see's that there is already a key present, and it is in process, it tells the later request that there exists a request

but what if two requests are parallel, how do we handle that case, because there the first request reads the db, and sees that there is no entry, and the second request sees the db before the key is inserted, in this case two requests start processing, how to solve this??? using critical section

basically we use locking based on the idempotency id, so as the two requests have the same key, they cant acquire the lock at the same time, so the second request wait till the lock is there, when the lock is released, it then check if in the db this key is already present, as the key is already present, it will return the previous response

but what if two requests are parallel, and they go to different servers, and they read from different DBs??? it might take minutes before the dbs get synced, what should we do in such cases???? we use a cache like redis, and store the key in redis, instead of reading from db, now the locking and reading all happens through redis

Important things to notice here are in case of parallel requests coming and checking the db if the key is present or not, we can remove this step, and we can make this atomic instead of using two steps like check and insert, we try to insert, if it is not present in db, it will be inserted and if the insert fails because the id should be unique, then we know that the key already exists, we return the previous response
