tar -zxf kafka_2.13-2.8.2.tgz
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
