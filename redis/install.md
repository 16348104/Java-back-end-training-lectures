# Chapter 2 Install

1. Ubuntu 下安装

```
$sudo apt-get update
$sudo apt-get install redis-server
```

启动 Redis

```
$ redis-server
```

查看 redis 是否启动？

```
$ redis-cli
```

以上命令将打开以下终端

```
redis 127.0.0.1:6379>
```

```
redis 127.0.0.1:6379> ping
PONG
```