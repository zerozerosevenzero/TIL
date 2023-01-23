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
  
