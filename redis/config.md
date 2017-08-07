# Chapter 3 Redis 配置

> 获取 CONFIG GET 命令

```
redis 127.0.0.1:6379> CONFIG GET <CONFIG_SETTING_NAME>
```

```
redis 127.0.0.1:6379> CONFIG GET loglevel
```

```
redis 127.0.0.1:6379> CONFIG GET *
```

> 设置 CONFIG SET 命令

```
redis 127.0.0.1:6379> CONFIG SET <CONFIG_SETTING_NAME> <NEW_CONFIG_VALUE>
```

```
redis 127.0.0.1:6379> CONFIG SET loglevel "notice"
OK
redis 127.0.0.1:6379> CONFIG GET loglevel
```