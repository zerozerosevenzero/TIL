# ECS(elastic container service)
컨테이너화된 애플리케이션의 손쉬운 배포, 관리 및 크기 조정에 도움이 되는 완전 관리형 컨테이너 오캐스트레이션 서비스

- AWS의 컨테이너 오케스트레이션 서비스
- 컨테이너를 실행하고 배포하고 관리

## 두 가지 모드
EC2: ec2를 활용한 컨테이너 서비스
Fargate: Serverless 컨테이너 서비스

## AWS Elastic Kubernetes Service(EKS)
 - AWS가 제공하는 kubernetes를 활용한 컨테이너 관리 시스템
 
## 다른 서비스와 연동가능
ECR(elastic container registy) aws의 DockerHub 컨테이너 이미지를 저장하는 용도
ALB(Application Load Balancer), CloudWatch

## EC2 VS ECS Fargate
EC2
 - 직접 관리 필요(스케줄링)
 - VPC 안에 생성
 - 주로 대규모의 어플리케이션에 사용
 - 비용이 많이 소모

Fargate
 - Serverless
 - VPC 밖에 생성되어 VPC에서 접근
 - 대규모 어플리케이션과 단기 작업에 사용
 - 비교적 비용관리가 쉬움


