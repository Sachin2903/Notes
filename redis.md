# Redis ( Inmemory store )

need to install redis ( PORT 6379 ) and redis stack ( GUI )

> production

>> docker run -d --name redis-stack-server -p 6379:6379 -p 8001:8001 redis/redis-stack-server:latest

> develop

>> docker run -d --name redis-stack -p 6379:6379 -p 8001:8001 redis/redis-stack:latest

---> this will pull the image and run

-d: Runs the container in the background (detached mode).
--name: Assigns a custom name (redis-stack) to the container for easier

>> sudo docker exec -it container_id bash

>> redis-cli ping
>> --> to run command on redis cli

> redis-cli
> --> go inside redis cli and no need to type again and again redis-cli

#### Data type in redis

## String

>> set keyname data
>> set name sachin

>> mset key value key2 value2
>> --> set multiple value at a time

>> get keyname
>> get name

>> mget key1 key2 key3
>> --> multiple get

--> key naming convention
<entity>:<id>

###### nx

set msg:1 hey nx
--> with nx . this will set value only if it does not exist

###### xx


###### ex , px expire pexpire

--> Can set the expire

set key value ex second
set ket value px millisecond 
expire key second
pexpire key millisecond

###### incr

incr count
--> to increment a count

incrby count 5

###### decr

decr count
decrby count 5

###### SUBSTR

SET mykey "Hello, Redis!"
SUBSTR mykey 0 4 # Returns "Hello"
SUBSTR mykey 7 11 # Returns "Redis"
SUBSTR mykey 0 -1 # Returns the entire string: "Hello, Redis!"

###### GETRANGE

SET mykey "Hello, Redis!"
GETRANGE mykey 0 4 # Returns "Hello"
GETRANGE mykey 7 11 # Returns "Redis"
GETRANGE mykey -6 -2 # Returns "Redis" (negative indices count from the end)
GETRANGE mykey 0 -1 # Returns the entire string

###### SETRANGE

SET mykey "Hello, World!"
SETRANGE mykey 7 "Redis" # Updates value to "Hello, Redis!"

SET mykey "Hello"
SETRANGE mykey 10 "World" # Sets value to "Hello\0\0\0\0World"

## List
redis list is an array can be used as stack , queue

* LPUSH RPUSH
* LPOP RPOP
* LLEN -> length of the list
* LMOVE -> atomically moves element from one list to another 
* LTRIM -> reduces a list to a specific range of element
* LRANGE -> get value of specific range
>> LRANGE mylist 0 -1
* LINDEX -> get value of specific range
>> LINDEX mylist 0

blocking commands
BLPOP -> block/wait of a seconds to pop and element if list is empty
>> BLPOP message 10(seconds)
BLMOVE ->

>> lpush list_name value
lpush messages hey
rpush messages hey

#### delete a key in redis
>> del key_name


#### return specific keys
>>  KEYS key_name:*

## Sets ( it donot add same member , not even update it )
* SADD
>> saad ip 1
>> saad ip:bikes:racing bike:1 bike:2

* SREM
>> srem ip 1

* SISMEMBER
>> sismember ip 3

* SINTER ->  return common members from 2 or more sets
>> 

* SCARD -> retuen a size of the set

## Hashmaps
hset biek:1 mode demimos brand erer type "asd asd " price 2555
```js
const fields=await client.hset(
    "bike:1",
    {
        model1:"demimos",
        brand:"ergonom",
        type:"fre",
        proce:5666
    }
)
hget("bike:1","price")
hgetall("bike:1")
hmget("bike:1",["model","price"])
hIncBy("bike:1","price",-100) or 100
```

## sorted sets ( Priority Queue )
zadd score 10 piyush
zadd score 1 john
zadd score 2 jane

sorted set

zrange score 0 -1
zrevrange score 0 -1
zrank score piyush 
this return the rank in the sorted sets

## redis streams
* XADD
* XREAD
* XRANGE
* XLEN




















# Redis with Node js

> > npm i ioredis

--> client.js

```js
const { Redis } = require("ioredis");
const client = new Redis();
module.exports = cliet;
```

--> string.js

```js
const client =require("./client")

async function init() {
  const result = await client.get("ket_name");
  awiat client.expire("keyname",seconds);
  await client.set("key","value");
}
```



# caching in nest js

>> npm install @nestjs/cache-manager cache-manager

CacheModule from nestjs/cache-manager

import in app.module.ts
imports:[
  CacheModule.register({
    max:100, // maximum number of keys
    ttl:0,
    isGlobal:true // to make it global in al module
  })
]

ttl -> 0 not expire
if use cache manager 4. version ttl should be in second and obove this have to use miniseconds

in service 

import Cache from "cache-manager";

constructor (@Inject(CACHE_MANAGER) private cacheManager:Cache){
     this.cacheManager.set(key,value)

     await this.cacheManager.get(key)

     .del(key)

     .reset() / reset cache

     .store.keys()  // get all keys 
}

// auto cache data 


* @UseInterceptors(CacheInterceptor)
class ABC{

}

@CacheKey("user")
* @UseInterceptors(CacheInterceptor)
async getALlUser

>> npm i cache-manager-redis-store@2
// allow us to use redis with cache manager

>> npm i @types/cache-manager-redis-store

in app module
import * as redisStore from "cache-manager-redis-store";

imports:[
  CacheModule.register({
    max:100, // maximum number of keys
    ttl:0,
    isGlobal:true // to make it global in al module
    store:redisStore,
    host:"172.17.0.1",
    port:"6379"
  })
]

```js
You can manually specify a TTL (expiration time in seconds) for this specific key, as follows:

await this.cacheManager.set('key', 'value', 1000);

To disable expiration of the cache, set the ttl configuration property to 0:



await this.cacheManager.set('key', 'value', 0);
```

@CacheKey('custom_key')
  @CacheTTL(20)