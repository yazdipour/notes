# Redis

https://redis.io/commands/

## Basics

```rs
ECHO 'Hi'
SET key value
GET key
INCR key
DECR key
FLUSHALL //remove all
DEL key
EXPIRE key 5 // expires after 5 sec
TTL key //Time to live of the obj (-1) if never expires
SETEX key 5 value // Set value and expiration at a same time
PERSIST key // remove the exiration
MSET key1 value1 key2 value2
APPEND key1 value1 //append to the end of the previous key1 value
```

## Persistence

https://redis.io/topics/persistence

Run redis with `--appendonly yes`

or

```rs
<!-- Snapshotting -->
SAVE // save snapshoot
SAVE 60 1000 // this configuration will make Redis automatically dump the dataset to disk every 60 seconds if at least 1000 keys changed
```

## LIST

```redis
LPUSH key value1 // add to the begining
RPUSH key value2 // add to the end
LRANGE key 0 -1 //return all items in the list
LLEN key //length of the list
LPOP key // Left pop
RPOP key
LINSERT key BEFORE value1 value2
```

## SETS

```redis
SADD key value
SISMEMBER key value // check if value is inside set
SMEMBERS key //shows all
SCARD key // cardinality of the set
SMOVE key1 key2 value1 // rm value1 from key1 and add it to key2
```

## SORTED SET

Sorted based on score number

```redis
ZADD key #score value //Adds all the specified members with the specified scores to the sorted set stored at key. It is possible to specify multiple score / member pairs. If a specified member is already a member of the sorted set, the score is updated and the element reinserted at the right position to ensure the correct ordering.
ZRANK key value //Returns the rank of member in the sorted set stored at key, with the scores ordered from low to high.
```

## Hashs

```redis
HSET [key] [field] [value]
HSET user name "ali"
HSET user:ali name "ali"
HSET user:ali phone "0923000000"
HGET user:ali name
HGETALL // return fields and their values
HMSET user:ali name "ALi" phone "058888" // multiple
HVALS user:ali // return values without fields name
HDEL user:ali age
```
