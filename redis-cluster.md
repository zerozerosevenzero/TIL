## 레디스 클러스터 

클러스터 설정파일
- cluster-enabled <yes/no>: 클러스터 모드로 실행할지 여부를 결정
- cluster-config-file <filename>: 해당 노드의 클러스터를 유지하기 위한 설정을 저장하는 파일로, 사용자가 수정하지 않음
- cluster-node-timeout <milliseconds> : 
  - 특정노드가 정상이 아닌 것으로 판단하는 기준 시간
  - 이 시간동안 감지되지 않는 master는 replica에 의해 failover가 이루어짐
- cluster-replica-validity-factor <factor> :
  - master와 통신한지 오래된 replica가 failover를 수행하지 않게 하기 위한 설정
  - (cluster-node-timeout * factor) 만큼 mater와 통신이 없었던 replica는 failover 대상에서 제외된다.
- cluster-migration-barrier <count>:
  - 한 master가 유지해야하는 최소 replica의 개수
  - 이 개수를 충족하는 선에서 일부 replica는 replica를 가지지 않는 master의 replica로 migrate 될 수 있다.
- cluster-require-full-coverage <yes/no>:
  - 일부 hash slot이 커버되지 않을 때 write 요청을 받지 않을지 여부
  - no로 설정하게 되면 일부 노드에 장애가 생겨 해당 hash slot이 정상 작동하지 않더라도 나머지 slot에 대해서 작동하도록한다.
- cluster-allow-reads-when-down <yes/no> :
  - 클러스터가 정상 상태가 아닐 때도 read 요청은 받도록 할지 여부
  - 어플리키이션에서 read 동작의 consistency가 중요치 않은 경우에 yes로 설정할 수 있음
  
# 클러스터 실습
 ## 1. redis.conf 파일 각 폴더에 저장 
  (7000/redis-7000.conf, 7001/redis-7001.conf, 7002/redis-7002.conf, 7003/redis-7003.conf, 7004/redis-7004.conf, 7005/redis-7005.conf)
  ```
  cp redis.conf 7000/redis-7000.conf)
  port 6379 -> port <port>
  cluster endabled yes
  ```
  ![image](https://user-images.githubusercontent.com/46700734/214085680-d80f43a5-f4ef-423e-a95e-723c53aadb41.png)

 ## 2. 각 클러스터 레플리카 설정하기
  ```
  redis-cli --cluster create localhost:7000 localhost:7001 localhost:7002 localhost:7003 localhost:7004 localhost:7005 --cluster-replicas 1
  ```
  
  ![image](https://user-images.githubusercontent.com/46700734/214086696-b13ecd9c-e50b-46ab-9d6c-7eff70bce100.png)
  - master 3개 
  - 7004의 master 7000
  - 7005의 master 7001
  - 7003의 master 7002
  - 생성완료
  - hash slot 16384개가 모두 커버되고 있는 상태
  ![image](https://user-images.githubusercontent.com/46700734/214087674-5f1b12cc-01e9-4bec-a089-fee073226a76.png)

  
 ## 3. 각 노드 상태 확인하기
  redis-cli -p 7000
  cluster nodes 
  ![image](https://user-images.githubusercontent.com/46700734/214088680-f562a6d5-4e5d-4dfc-b634-3308f86b1b60.png)

  7003에서
  ```
  set aaa dd
  ```
  ![image](https://user-images.githubusercontent.com/46700734/214089133-a63af242-5787-4266-a68d-de82b12002ce.png)

  7001의 slave 7003 readonly속성 변경
  ```
  get aaa -> 실패
  readonly
  get aaa -> 성공
  ```
  
 ## 4. 7001번(마스터 노드) 종료시키기(failover상태 만들기)
  7000번에서 다시 노드 상태 확인
  ```
  cluster nodes
  ```
  ![image](https://user-images.githubusercontent.com/46700734/214091254-cbcd438d-ca97-456a-94a5-8e86cc6c62e3.png)

  - 7001 죽은 것 확인
  - 7003 마스터로 승격
  - 7003에서 set 명령어를 통해 수행 시 정상 동작 
  ![image](https://user-images.githubusercontent.com/46700734/214091560-76277e9b-7190-494f-afb3-0a915274047f.png)
 
 ## 5. 7001 (이전마스터노드) 다시 실행
  ```
  redis-server ./redis-7001.conf
  ```
  - 7003 마스터 유지
  - 7001 slave로 소생
  ![image](https://user-images.githubusercontent.com/46700734/214092487-62cdf8e4-ac0a-4acf-9c5e-e8c1c0293929.png)

  
## 6. 7006 신규노드 기존 클러스터에 추가하기
  ```
   cp redis.conf 7006/redis-7006.conf)
   port 6379 -> port <port>
   cluster endabled yes
  ```
  
  7006을 7001의 클러스터에 삽입 7001이 아닌 다른 노드여도 상관없음
  ```
  redis-cli --cluster add-node localhost:7006 localhost:7001
  ```
  
  마스터로 생성
  ![image](https://user-images.githubusercontent.com/46700734/214094412-91d25fdd-1f8b-48ce-b7d4-d0fe8396018d.png)

## 7. 7006의 replica 7007 추가하기
  - 7001 생성
  ```
   cp redis.conf 7007/redis-7007.conf)
   port 6379 -> port <port>
   cluster endabled yes
  ```
  
  - 기존 클러스터에 삽입하는데 7006의 slave로 삽입
  ```
   redis-cli --cluster add-node localhost:7007 localhost:7006 --cluster-slave
   redis-cli --cluster add-node localhost:7007 localhost:7006 --cluster-slave ${여기에 마스터로 놓일 곳 정하는 것도 가능}
  ```

  - 7007 slave로 삽입된 것 확인
  ![image](https://user-images.githubusercontent.com/46700734/214095808-90a767c3-dffa-4da6-bfc1-4c593fbee4cd.png)

  
  
