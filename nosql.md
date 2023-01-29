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

