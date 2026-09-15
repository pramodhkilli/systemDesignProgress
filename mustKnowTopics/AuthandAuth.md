# authentication and autherization

so first, lets say, i have a server for my business, which has some users, when someone calls a api from the ui, know dont know who is calling and what information particular to that user i have to give, so i have to collect the user identity

but what if someone is masking themselves and pretending to be the user when they are not, so we have to first authenticate then, if they are a proper user, let's say if the username is correct or not, or if the password is correct or not for that username, something like

okay this part is done, but http is stateless, it does not store any record or state of the previous calls, so then how can i stay logged in to my server

this is where sessions, jwt come into picture

session : let's say after we authenticate the user credentials, we return a sessionId, which has some time to live, and in every subsequent calls, browser sends this sessionId through the cookies, now i store the user related information for that sessionId in my db, or file system or redis, when a request comes, i check user details against that session id, and load user specific information like items in a cart or something like that, but this kind of makes the servers stateful, which makes it difficult to scale, because when a server which is storing my session id fails, i have to go to a different server, in which my details are not stored, it may not sound like much, but this effects the user experience, you may think that we can have a distributed redis cache and store them there, but our next solution solves that problem with a smart solution

JWT : json web tokens
jwt essentially has 3 parts, header which contains information about the encryption algorithm, the actual body which contains informatino about the user like the id, role, and the last part is the signature which is made by the server using a asymmetric cryptographic algorithm

the browser does not have any of the keys, so it cannot produce signature from the header and payload, the server has both the keys, private and public, so even if i change some information like my role and send the request the signature will be the same, when the server verifies this by producing the hash against the payload and header, it wont match with the signature

if both the keys are not visible to the browser why not use symmetric cryptography???? valid question, but what if i need to share this key with my other services, which also want to authenticate a request going to them, now if i had used symmetric hashing, then i have to share this key, which could be lost and used to decrypt bearer tokens of users, that is why we use asymmetric hashing, we share the public key to other services, even if the public key is lost, it does not effect anything

Now what is authorization:

we solve the part where we ask the user, are you really who are claiming to be??? but what about does this user have access to this information, just because they have authenticated does not give them the power to see all our data, which could be sensitive

here we have role based access control, when admin has some rights, user has some rights

resource based access control, so based on who logged in, this changes, i can see my profile, but i cannot see someone else's profile

and these can be complex as well, like for suppose i work in the finance department in my company, and my role is a manager, so i should have access to finance department related data that too till what the manager could see, i should not be able to see developers related sensitive information
