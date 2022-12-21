# Redis 공부 내용 정리


### redis 컨테이너 실행
```
docker run --name ${} -p 6379:6379 redis
ex) docker run --name my-redis -p 6379:6379 redis
```

### 도커 컨테이너 안에서 쉘 실행
```
docker exec -it my-redis /bin/sh
redis-cli
set key1 banana
get key1
dbsize   # db size 
flushall # db 날리기
```

### String
| 명령어 | 기능 | 예제
|---|---|---|
|SET | 특정 키의 문자열 값을 저장한다||
|GET | 특정 키의 문자열 값을 얻어온다||
|INCR | 특정 키의 값을 INTEGER로 취급하여 1 증가시킨다. ||
|DECR | 특정 키의 값을 INTEGER로 취급하여 1 감소시킨다.||
|MSET| 여러 키에 대한 값을 한번에 저장한다.|MSET key1 milk key2 coffee|
|MGET| 여러 키에 대한 값을 한번에 얻어온다.|MGET key1 key2|

### List
 - Linked-list 형태의 자료구조
 - Queue와 Stack으로 사용할 수 있음
 - http://redisgate.kr/redis/command/lists.php (명령어모음)

| 명령어 | 기능 |
|---|---|
|LPUSH ||
|RPUSH ||
|LLEN ||
|LRANGE ||
|LPOP||
|RPOP||

### SET

![image](https://user-images.githubusercontent.com/46700734/208946355-9f84747f-07a9-491a-b555-eae7284291f6.png)


