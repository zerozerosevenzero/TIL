NAT Gateway/ NAT Instance
 - Private 인스턴스가 외부의 인터넷과 통신하기 위한 통로
 - NAT Instance는 단일 EC2 인스턴스 / NAT Gateway는 AWS에서 제공하는 서비스
 - NAT Gateway/Instance는 모두 서브넷 단위
  - public subnet에 있어야함
 
 Bation Host
 - 외부에서 사설 네트워크에 접속할 수 있도록 경로를 확보해주는 서버
 - private 인스턴스에 접근하기 위한 EC2 인스턴스
 - public 서브넷에 위치해야함
