# Chapter 4 Redis 数据类型

1. string 字符串

```
redis 127.0.0.1:6379> SET key "value"
OK
redis 127.0.0.1:6379> GET key
"value"
```

2. hash 哈希

```
127.0.0.1:6379>  HMSET test key1 "value1" key2 "value2"
OK
127.0.0.1:6379>  HGETALL test
```

3. list 列表
4. set 集合
5. zset 有序集合