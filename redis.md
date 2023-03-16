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


## redis rdb로 db 백업하기 
redis.conf는 https://redis.io/docs/management/config/ 여기서 다운받아 경로에 저장 후 -v 옵션으로 실행
```
docker run -v $(pwd)/redis.conf:/redis.conf —-name my-redis-with-config redis redis-server /redis.conf
```

redis 값 rdb에 dump 파일로 저장

특정 주기마다 변경하고 싶을 때
(ex) 60초에 10개 이상 변경될 시 스냅샷에 저장 
```
code redis.conf
```
![image](https://user-images.githubusercontent.com/46700734/212547152-0dcd0316-d6fc-40a4-932b-ff20a14b5670.png)

## 수동으로 스냅샷 저장

redis-cli 들어가서 bgsave
```
bgsave
```

## AOF(Append Only File)를 사용한 백업

### AOF란..?
- 모든 쓰기 요청에 대한 로그를 저장
- 재시작 시 AOF에 기록된 모든 동작을 재수행해서 데이터를 복구

### AOF의 장점
- 모든 변경사항이 기록되므로 RDB 방식 대비 안정적으로 데이터 백업 가능
- aof 파일은 append-only방식으로 백업파일의 손상될 위험이 적음
- 실제 수행된 명령어가 저장되어 있으므로 사람이 보고 이해할 수 있고 수정도 가능

### AOF의 단점
- RDB 방식보다 파일 사이즈가 커짐
- RDB 방식 대비 백업 & 복구소도가 느림 (fsync 정책에 따라 달라짐)

AOF 설정


AOF 사용 (기본값은 no)
redis.conf에서 기존 save 옵션은 
![image](https://user-images.githubusercontent.com/46700734/212711483-beb409e1-8c4a-4b68-854d-a594e82fc2b7.png)


```
appendonly yes
```

AOF 파일 이름
```
appendfilename appendonly.aof
```

fsync 정책 설정
```
appendfsync everysec
```

fsync 정책(appendfsync 설정값)
- fsync 호출은 os에게 데이터를 디스크에 쓰도록 함
- 가능한 옵션과 설명
- always: 새로운 커맨드가 추가될 때마다 수행, 가장 안전하지만 느림
- everysec: 1초마다 수행, 성능은 RDB 수준에 근접
- no: OS에 맡김. 가장 빠르지만 덜 안전한 방법(커널마다 수행시간이 다를 수가 있음)

## redis의 복제(replication)

Replica 노드에서만 설정을 적용해 master-replica 복제 구성 가능

replica로 동작하도록 설정
```
replicaof 127.0.0.1 6379
```

replica 속성 변경
```
replica-read-only
```

마스터 노드에는 RDB나 AOF를 이용한 백업 기능 활성화가 필수!

--- 

Redis Data Type
Sorted Sets(ZSET)

ZADD: 입력
ZCARD: Count
ZRANGE: 정렬순서로 조회
ZRANGEBYSCOE: score로 함께 조회
ZREM: 삭제
ZSCORE: 특정 member의 score를 조회
ZRANK: 특정 member의 rank를 조회





