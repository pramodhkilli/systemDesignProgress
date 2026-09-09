# how data is stored in disc in postgres

so, normally when you see a table, you think that the table is stored in a file in the file system, what else could even happen???

nahh bro, the internal framework is such that for a single table there can be multiple files

each file can have multiple page, in postgres page is where the data is stored along with some metadata for the page, so to fetch some data, we need to go to these pages and fetch them

and each page can have multiple tuples(tuple is how your row is stored in the page)

page structure :

lets say a page has some number, that uniquely identifies the page, and from the top we have pointers, and from the bottom of that page we store the tuples

metadata
________

ptr 1
ptr 2
ptr 3
.
.
.
Free Space
.
.
.
tuple 3
tuple 2
tuple 1

this is how the data is stored in the page, each page is of size 8kb, and each tuple can be of variable sizes

CTID :

ctid is the combination of the page number and the tuple position
