# PostMaster

consider postgres as a client server architecture, postmaster is the one listening, and clients are the connections we make to the DB, so generally the port 5432 is used by postgres, so postmaster listens on this port, then when a connection is made, it kind of creates a subprocess and run the query or whatever the process needs

postmaster is a infinite loop listening or waiting for incoming connections
