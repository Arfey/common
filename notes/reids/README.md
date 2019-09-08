# Redis

Redis is in-memory data structure store. Very often redis use as database, cache or message broker.

___

List of possible data types:

- string (binary)
- hash
- set 
- list
- sorted set
- bitmaps / HyperLogLog

# Use cases

- **String**

  - `Full page cache (FPC)`. The best way to improve speed of response from your server is cache it. 
  A string in redis very good for full page cache. When u get request you  need to get a path and 
  check if this key exist in redis if it does, u need to return value of this key as response, else 
  render page by your backend return page and set page to the redis with some ttl.
  - `Counting stuff`. U can use INCR/DECR to counting something.
  - `Locking`. Sometime u need to lock some process between your web workers and redis can 
  to help with that.  If u wanna lock some function u can before start this function checking if exist 
  some key in redis and if exist do nothing, else set this key in redis, run function and after complite 
  u need delete key from redis.
  - `Throttling`. If you wanna throttling some process u can do the same as with locking but without removing
  key instead of that u need to set ttl for this key. 
  
  **Set**

  - `Scaling and parallel processing` data is also possible with redis set. 
  You can put in `set` list of data that you need to processing and after 
  that run big count of workers that will be get part of data use pop method
  and do something with it. It's good approach when you need to do some with
  a big batch of instances from db. You put list of id to set and after that 
  run some count of workers (celery task) when u use the pop method to get data
  and if this method return null u stop to do, else processing data and 
  repeat again.
  - `Message broker`. You can use redis as message broker.
  - `Unique N items`. Whan u need to have a list with unique items.
  
  **Hash**
  
  - `Session Cache`. The redis is so fast. Also he offers persistence unlike memcached, so Redis is a 
  good solution for store user's session data.
  
  **Sorted set**
  
  - `Top 10`. You can add to sorted set items with rank and after that use ZREVRANGE command for return 
  top N elements.
  - `Task Scheduling`. U can use sorted set for make scheduling tasks. For that u need set score to unix time.
  
  **Pub / Sub**
  
  - todo


# References

- https://redislabs.com/blog/
- https://www.youtube.com/channel/UCD78lHSwYqMlyetR0_P4Vig/videos
