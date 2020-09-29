Main Question:
    Design a distributed counter

Similar Question:
- Number of likes on Facebook
- Number of retweets on Twitter
- Number of shares traded on an exchange
- Clicks, views, etc


Answer:
solution 1:
    Use a lock with RDMBS
    Use multiple locks, instead of one. Split one counter into multiple sub-counters. Each writer choose one to update. Then sum them up. Thus less frequent locking might happen.
    Link: https://firebase.google.com/docs/firestore/solutions/counters

solution 2:
    Use MQ + batch updates. Serialize all updates requests into a queue. Then use a single write strategy to update it. When update the counter, batch multiple updates as one.

solution 3:

    Use existing solution. Twitter use rainbird for real-time analytics. Rainbird is a distributed, high-volume counting service built on top of Cassandra. 
    Link: https://www.slideshare.net/kevinweil/rainbird-realtime-analytics-at-twitter-strata-2011

solution 4:
    keep the system in different shrad and while updating into different shrad, use queues
    while sending the total counter read it from different shrad and sum it up
    