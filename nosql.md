## RDBMS, MongoDB 비교 
|RDBMS|MongoDB|
|-----|-----|
|Table|Collection|
|Row|Document|
|Column|Field|

## 기본 특징
- Database > Collection > Document > Field

## Database 특징
- admin: 인증과 권한부여의 역할
- local: 
    - 모든 mongo instance는 local database를 소유한다.
    - oplog와 같은 replication 절차에 필요한 정보를 저장한다.
    - startup_log와 같은 instance 진단정보를 저장한다.
    - local databaes 자체는 복제되지 않는다.
 - shard: sharded cluster에 각 shard의 정보를 저장한다.
   
## Collection 특징
- 동적 스키마를 갖고 있어서 스키마를 수정하렴녀 필드값을 추가/수정/삭제하면 된다.
- Collection 단위로 index를 생성할 수 있다.
- Collection 단위로 Shard를 나눌 수 있다.

## Document 특징
- JSON 형태로 표현하고 BSON(Binary JSON) 형태로 저장한다.
- 모든 Document 에는 "_id" 필드가 있고, 없이 생성하면 ObjectId 타입의 고유한 값을 저장한다.
- 생성 시, 상위 구조인 Database나 Collection이 없다면 먼저 생성하고 Document를 생성한다.
- document의 최대 크기는 16mb 이다.

## Replica Set
 Replica Set은 HA솔루션이다.
 데이터를 들고 있는 멤버의 상태는 Primary와 Secondary가 있다.
 Secondary는 선출을 통해 과반수의 투표를 얻어서 Primary가 될 수 있다.
 - Primary:
    - read/write 요청 모두처리할 수 있다.
    - Write을 처리하는 유일한 멤버이다.
    - Replica Set 하나만 존재할 수 있다.
 
 - Secondary:
    - Read에 대한 요청만 처리할 수 있다.
    - 복제를 통해 Primary와 동일한 데이터 셋을 유지한다.
    - Replica Set에 여러개가 존재할 수 있다.
 
 - Arbiter:
    - data를 들고 있지않고 Primary선출에만 관여하는 멤버
 
 - oplog:
    - Replica Set의 모든 멤버가 동일한 데이터셋을 이룰 수 있도록함
    - local database의 Oplog Collection을 통해 복제를 수행한다.    

---
## Shard Cluster
 - 모든 Shard는 Replica Set으로 구성되어 있다.
 - Sharding: 큰 데이터를 여러 데이터로 분할하는 과정
 - Shard: 분할된 데이터셋, Collection 단위로 샤딩이됨
 - Shard key: 분산이 되는 기준
 - Sharding은 Shard Key를 선정해야하고 해당필드에는 Index가 만들어져 있어야한다.
 - **Replica(복제)는 HA를 위한 솔루션이고 Sharding은 scale out을 위한 분산처리를 위한 솔루션**

## Shard cluster의 장단점
    - 장점:
        - 용량의 한계를 극복할 수 있다.
        - 데이터 규모와 부하가 크더라도 처리량이 좋다.
        - 고가용성을 보장한다.
        - 하드웨어에 대한 제약을 해결할 수 있다.
    - 단점:
        - 관리가 비교적 복잡하다.
        - Replica Set과 비교해서 쿼리가 느리다.

## Sharding vs Partitioning
  - Sharding: 하나의 큰 데이터를 여러 서브셋으로 나누어 여러 인스턴스에 저장하는 기술 
  - Partitioning: 하나의 큰 데이터를 여러 서브셋으로 나누어 하나의 인스턴스의 여러 테이블로 나누어 저장하는 기술
  
## Replica Set vs Sharded Cluster
  - Replica Set은 각각 멤버가 같은 데이터 셋을 갖는다.
  - Sharded Cluster 각각 Shard가 다른 데이터 서브셋을 갖는다.
  
## Sharding 전략

   1. Ranged Sharding: 값의 범위에 따라 샤딩, 값이 몰리는 경우가 발생할 수 있음
   2. Hashed Sharding: 해쉬 함수를 이용한 샤딩
   3. Zone Sharding: 특정샤드로 배치시킬 수 있는 방법, Ranged, Hashed 샤딩과 같이 사용함

## Replica Set vs Sharded Cluster
 Replica Set
   - 운영이 쉽다.  
   - 장애발생 시 문제해결 및 복구가 쉽다.  
   - 서버 비용이 적게든다.  
   - 성능이 좋다.  
   - 개발 시 설계가 용이하다.  
   - Read에 대한 분산이 가능하지만, Write에 대한 분산은 불가능하다.  

 Sharded Cluster
   - Scale-Out이 가능하다. 
   - Write에대한 분산이 가능하다. 
   - Replica Set의 모든 장점이 상대적으로 단점이된다. 

---

# Standard Connection String format 사용하기

## local mongodb 접속
```
mongosh "mongodb://localhost:27017"
```

## Replica Set인 경우
```
mongosh "mongodb://localhost:27017,localhost:27018,localhost:27019"
```

## db이름이 myDatabase인 경우
```
mongosh "mongodb://localhost:27017,localhost:27018,localhost:27019/myDatabase"
```

## replicaSet 및 maxPoolSize 정의 
```
mongosh "mongodb://localhost:27017,localhost:27018,localhost:27019/myDatabase?replicaSet=rs1&maxPoolSize=1000"
```

---

# SQL VS MQL
 
 select * from table;
 db.collection.find({});
 
 ## sql-to-mongodb-mapping-chart
 https://www.mongodb.com/docs/manual/reference/sql-comparison/














  
 


