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
  

