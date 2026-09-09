# how connections are made in postgres

so, normally we might think that if a client calls a database, it establishes a connection, and then if the query is returned, the connection is terminated, but that is not what is happening here, so there is a concept of connection pools, when a request is made, we go to the connection pool like hikariCP, it gives us a connection, then we use that connection and submit our sql, then postgres receives that at the postmaster, and creates a backend process, and then your query executes and the data is fetched or updated something
