# circuit breaker

so what the hell is this thing, sounds very scary, isnt it

lets say you have an application like zomato, and you have a flow like client -> order service -> payment service

what if payment service fails???, order service will keep sending the requests to the payment service, they will be getting timed out, which makes every request coming to the order service to time out, but the requests to the order service keeps coming, so order service will exhaust its threads, so it fails eventually, this is what is called a cascading failure

but how do we over come this???

this is where circuit breaker comes in, imagine if you have a clarity that the payment service is failing, instead of calling it, you could just simply not call it and return something like service unavailable or may be ask the users to pay via cash or something

this way the requests wont be going to the payment service

this is more or less what the circuit breaker does, so it keeps a statistical data of some configuration, like last x calls, how many failed, how many succeeded, on what threshold we should stop calling the payment service

once that threshold is hit, the circuit will be open(imagine like an electrical circuit, open is when current does not flow, close is when current flows), after some time, the circuit goes into an half-open state, in which the order service sends a small amount of calls to go to the payment service, and sees if the payment service is up and having less failure rate, if it is having less failure rate, then it will go to closed state again allowing requests to pass through, else it will again go the open state

                ┌──────────────┐
                │    CLOSED    │
                │ normal calls │
                └──────┬───────┘
                       │
              failures exceed
                 threshold
                       │
                       ↓
                ┌──────────────┐
                │     OPEN     │
                │ fail fast    │
                └──────┬───────┘
                       │
                 wait duration
                       │
                       ↓
                ┌──────────────┐
                │  HALF-OPEN   │
                │ test calls   │
                └──────┬───────┘
                    /       \
                 success    failure
                   /           \
                  ↓             ↓
              CLOSED          OPEN