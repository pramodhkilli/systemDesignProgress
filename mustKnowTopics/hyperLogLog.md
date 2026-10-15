# hyperLogLog

lets say you have a number stream or any stream strings or characters or something, you want to find the unique elements from this stream or a list of elements, how will you do it??

simple bro, just use a set, pass all the elements through this set, it will store only the unique elements, return the size of the set

what if you have billion elements????still doing the same set approach????

hyperLogLog is a very mathematical algorithm, lets say you have a hash function that spreads the output evenly, that mean the probability is equal for each number in the range

if suppose you see a has output, that has 4 leading zeros like 0000101101, something like this, the probability of this number coming with 4 leading zeros is 1/2^4, so can we approximate that to get a number having 4 leading zeros, we would have done roughly 2^4 generations???? yes we can

that is the base of this hyperloglog functionality

but what if i get 4 leading zeros on the first try??? it is possible, so this becomes a noice as variance could be high, so what we do is we take m buckets, and we kind of group our hashes into these buckets, and get the rank of these buckets individually, here rank is the maximum number of leading zeros

so, lets say i have taken m as 16, we need 4 bits to represent 16, 0-15, 0000 - 1111, so for every hashed binary number we take the first 4 bits and use it to send this number to its particular bucket

we have 16 buckets, so these 16 buckets have 16 ranks from their group

we take harmonic mean of these numbers to come to an average number

so mathematically harmonic mean = m/(sigma(i = 0 to m-1) 1/2^mi)

i wrote the word sigma, cause i could not insert the symbol

okay so we got the average, then to get the cardinality, what should be do?????

lets say the harmonic mean is x, then the cardinality will be a*m*x

where m is the number of buckets, and a is a constant and its value is around 0.7205

and fun fact is the name loglog comes because, for a cardinality of n, the maximum number of leading zeros would be log(n) and to store this value, we need a storage of log(log(n)) bits