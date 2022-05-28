VPC(Virtual Private Cloud)
사용자의 AWS계정 전용 가상 네트워크
EC2인스턴스와 같은 AWS리소스를 VPC에서 실행시킬 수 있음
가상의 데이터 센터
리전단위

VPC의 구성요소
 - 서브넷        
 - 인터넷 게이트웨이
 - NACL/보안그룹
 - 라우트 테이블 //트래픽이 어디로 가야할지 알려주는 이정표, VPC생성 시 기본으로 하나 제공
 - NAT instance/Gateway
 - Bastion Host
 - VPC Endpoint

VPC Peering
 - 두개의 다른 VPC를 연결하여 VPC안의 리소스끼리 통신이 가능하도록 설정하는것
 - 다른 리전, 다른 계정의 VPC끼리 연결 가능
 - CIDR Range 중첩 불가능
 - Transitive Peering 불가능
   - 통신을 위해서는 직접 연결되어야함
   - 혹은 Transit Gateway 이용

