Reliability is the probability that a system will perform its intended function correctly over a given period of time, under specified conditions.

This definition has several important parts.

"Correctly" means producing the right output, not just any output.
"Over a given period" means reliability is measured over time, not at a single instant.
"Under specified conditions" means we define what normal operation looks like.

Availability	    Is the system responding?	System returns HTTP 200
Reliability	        Is the response correct?	The balance returned is accurate
Fault Tolerance	    Does it keep working when components fail?	Works with one database replica down
Durability	        Is data preserved despite failures?	Data survives disk failure

A payment system that charges customers twice is available (it processes requests) but unreliable (it processes them incorrectly). A database that loses writes during failover is fault-tolerant (it continues operating) but not durable (data was lost).

Measuring Reliability
    1. Mean Time Between Failures (MTBF)
        MTBF measures the average time between failures. A higher MTBF means failures are less frequent.

        MTBF = Total Operating Time / Number of Failures

        Example: if a system ran for 10,000 hours and experienced 5 failures, MTBF = 10,000 / 5 = 2,000 hours.
    
    2. Mean Time To Recovery (MTTR)
        MTTR measures how long it takes to restore the system after a failure. A lower MTTR means faster recovery.

        MTTR = Total Downtime / Number of Failures

        Example: if 5 failures occurred and total repair time was 10 hours, MTTR = 10 / 5 = 2 hours per failure.

    3. Error Rate
        Percentage of requests that result in errors.

        Error Rate = Failed Requests / Total Requests × 100%

    4. Data Correctness
        Percentage of responses that contain correct data.

        Correctness = Correct Responses / Total Responses × 100%

Why Systems Become Unreliable
    Hardware failures
    software bugs
    configuration errors
    Human error
    Overload and cascading failures

Redundancy plus failover keeps the system serving when components die. An untested failover path is a false sense of safety.

Graceful degradation reduces blast radius. Core flows should keep working when optional services fail; emergency mode is better than a blank page.

Circuit breakers prevent one slow dependency from taking down the rest of the system. Fail fast, then recover deliberately.

Idempotency makes retries safe. Money-moving operations should require an idempotency key so duplicate requests do not cause duplicate effects.