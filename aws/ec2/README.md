### EC2 생명 주기
AMI -> pending -> rebooting-> running -> stopping -> stopped -> terminated

중지
 - 중지 중에는 인스턴스 요금 미청구
 - 단 EBS요금, 다른 구성요소 (Elastic IP)은 청구
 - 중지 후 재시작시 퍼블릭 IP 변경
 - EBS를 사용하는 인스턴스는 중지 가능: 인스턴스 저장 인스턴스는 중지 불가

재부팅
 - 재부팅시에는 퍼블릭 IP 변동 없음
최대 절전모드
 - 메모리 내용을 보존해서 재시작시 중단지점에서 시작할 수 있는 정지모드

