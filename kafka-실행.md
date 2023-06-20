tar -zxf kafka_2.13-2.8.2.tgz  
desktop/kafka_config 폴더 확인  
cd kafka_2.13-2.8.2
z kafka_2.13-2.8.2

## 주키퍼 실행
```
bin/zookeeper-server-start.sh config/zookeeper.properties
```

## Config파일 수정
vi config/server.properties
```
advertised.listeners=PLAINTEXT://localhost:9092
```

## 카프카 서버 실행
```
bin/kafka-server-start.sh config/server.properties
```

## 토픽 생성
```
bin/kafka-topics.sh --create --topic topic-example1 --bootstrap-server localhost:9092
```

## 토픽 정보
```
bin/kafka-topics.sh --describe --topic topic-example1 --bootstrap-server localhost:9092
```

## 카프카 프로듀서 실행
```
bin/kafka-console-producer.sh --topic topic-example1 --bootstrap-server localhost:9092
```

## 카프카 컨슈머 실행
```
bin/kafka-console-consumer.sh --topic topic-example1 --from-beginning --bootstrap-server localhost:9092
```

## 카프카 group명 임영
```
bin/kafka-console-consumer.sh --topic topic1 --group team-a --from-beginning --bootstrap-server localhost:9092

```

## 카프카 current offset 확인
```
bin/kafka-consumer-groups.sh --bootstrap-server=localhost:9092 --group team-a --describe
```

## 카프카 config 파일에서 server.properties 들 안에 옵션 값 확인하기
1. server.properties, server2.properties, server3.properties 값 설정 
![image](https://user-images.githubusercontent.com/46700734/209983550-7cc2df3c-0528-46ff-81f9-d182dd0e298f.png)

```
grep broker.id server*
grep listeners server*
grep log.dirs server* 
```
그림과 같이 확인 가능.   

<img width="623" alt="image" src="https://user-images.githubusercontent.com/46700734/209983747-abc5e3b3-b85c-43ea-8ac4-dba291d27f8d.png">


## 카프카 클러스터 구성하기
```
bin/kafka-topics.sh --create --topic topic2 --bootstrap-server localhost:9093 --partitions 3 --replication-factor 2
```

## 카프카 topic2에 연결
```
bin/kafka-console-producer.sh --topic topic2 --bootstrap-server localhost:9092,localhost:9093,localhost:9094
```

## server2.properties로 시작한 브로커죽이기
```
ps -ef | grep server2.properties 
pid 확인 후 삭제
```
