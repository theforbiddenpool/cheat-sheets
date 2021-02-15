__Redis__ → open-source, noSQL in-memory database. It's often used to build really high performance scalable web applications.

Redis is used for **short lived data** in our applications, *e.g.* sessions, web page headcounts. Being in-memory, we don't have large datasets - we have small pieces of data that are kept in memory, not on disk. This, in turn, means it's really fast.

It should only be used on data that **we don't care about losing** if there's an unexpected shutdown. However, Redis does take a snapshot once in a while, and saves it to the disk.

## Data Types
Redis suports five major different data types:
- __strings__
- __hashes__ → maps between string fields, and string values. They are similar to JavaScript objects.
- __lists__ → implemented as linked lists. Insertion is really fast, whilst searching takes longer than when using arrays. Useful for when we have long lists where we need to add elements quickly.
- __sets__ → unordered collection of strings. Repeated values are not allowed, avoiding any duplicates.
- __sorted sets__ → ordered collection of strings. Every member of the set is associated with a score, allowing us to order the set from smallest to greatest.

## CLI
#### Set a new Key-Value pair:
```
SET <key> <value>
```
- `MSET` → sets multiple keys at the same time.
- `HMSET` → creates a hash. *e.g.* `HMSET user id 45 name "Jonny"`
- `LPUSH`, `RPUSH` → pushes a value to a list, on the left or right, respectively. *e.g.* `LPUSH onelist 12`
- `SADD` → creates a set. *e.g.* `SADD firstset 1 2 3 4 5`
- `ZADD` → creates a sorted set. *e.g.* `ZADD secondset 50 "Wizards"`

#### Get the value of a key:
```
GET <key>
```
- `MGET` → getS multiple keys.
- `HGET` → gets a hash. *e.g.* `HGET user name`
- `HGETALL` → gets all the identifying criteries of a hash.
- `LRANGE` → grabs data from a list within the specified range. *e.g.* `LRANGE onelist 0 1`
- `SMEMBERS` → grabs all the members of a set.
- `ZRANGE` → grabs the members of a set within the specified range.

#### Check if a key exists:
```
EXISTS <key>
```
- `SISMEMBER` → check if a member exists within a set. *e.g.* `SISMEMBER firstset 5`

#### Delete a key:
```
DEL <key>
```

#### Set a key to expire after x seconds:
```
EXPIRE <key> <seconds>
```

#### Remove the last element from a list:
```
RPOP <list-key>
```

#### Get the rank of an element in a sorted set
```
ZRANK secondset "Wizards"
```

For more commands we can check their [documentation](https://redis.io/commands).

# Sources
[The Complete Junior to Senior Web Developer Roadmap (2020)](https://www.udemy.com/course/the-complete-junior-to-senior-web-developer-roadmap/), by Andrei Neagoie
