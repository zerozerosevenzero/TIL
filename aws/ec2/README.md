### EC2 생명 주기 05/22
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

### 보안그룹 05/22
보안 그룹은 인스턴스에 대한 인바운드 및 아웃바운드 트랙픽을 제어하는 가상 방화벽 역할

Port 허용
 - 기본적으로 모튼 포트는 비활성황
 - 선택적으로 트래픽이 지나갈 수 있는 Port와 source를 설정 가능
 - Deny는 불가능

인스턴스 단위
 - 하나의 인스턴스에 하나 이상의 보안 그룹 설정 가능
 - 인스턴스에 여러 보안 그룹이 적용될 경우 모든 보안 그룹의 규칙을 적용 받음


### EC2권한부여 05/23
sudo -s

aws ec2 describe-instances --region ap-northeast-2 //aws ec2인스턴스 목록을 보여줌 권한없이 불가
1. 설정정보를 통해 들어가기(사용자에게 ec2 full access 권한주고 key받은다음 접근)
aws configure // aws 설정정보
aws_access_key_id: .....
aws_secret_access_key: .....
 
2. IAM에 ec2 full access역할을 부여한후 접근

기타: vi ~/.aws/credentials // 1번으로 ec2접근 했을 경우 aws key와 secret-key확인 

### ENI(Elastic Network Interface) 05/23
- EC2의 가상의 랜카드
- IP주소와 Mac 주소를 보유
- 하나의 인스턴스에 여러개의 ENI를 연동가능
- 인스턴스 유형 및 사이즈에 따라 최대 보유 가능한 IP주소가 변동
- 내부적으로는 보안 그룹은 ENI에 부착

탄력적 IP
- EC2의 퍼블릭 IP를 고정해주는 서비스(즉, 인스턴스를 중지-> 재시작해도 고정적인 IP를 확보 가능
- 사용할때는 무료, 단 확보하고 사용하지 않을 경우 비용 발생
- EC2이외의 다른 서비스(NLB)에도 사용
- 내가 보유한 IP주소를 AWS에서 사용가능
- 리전 단위

### 스케일링
 - 수직확장(Scale Up): 더 좋은 리소스로 확장
 - 수평확장(Scale Out): 더 많은 리소스로 확장

### EC2 Auto Scaling
 - 정확한 수의 EC2 인스턴스를 보유하도록 보장
 - 가용 영역에 인스턴스가 골고루 분산될 수 있도록 인스턴스를 분배
 - 구성(시작 구성, 모니터링, 설정)






