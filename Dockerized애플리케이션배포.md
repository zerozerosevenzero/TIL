### maven 빌드 방식, ec2(cent OS)

## 1. intellij 프로젝트파일에 Dockerfile 생성

```
FROM openjdk:8-jdk-alpine
ARG JAR_FILE=target/*.jar
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-jar","/app.jar"]
```

## 2. 도커 이미지 만들기
터미널창에 다음과 같이 입력
```
maven: docker build -t {도커사용자이름}/{애플리케이션이름} .
gradle: docker build --build-arg JAR_FILE=build/libs/\*.jar -t springio/gs-spring-boot-docker .
(ex) docker build -t sgs1159/new-app .
```

## 3. 도커이미지 실행시키기
```
docker run -p 8080:8080 {도커사용자이름}/{애플리케이션이름}
```

## 4. 도커허브에 등록하기
```
https://hub.docker.com/
```
```
docker push {도커사용자이름}/{애플리케이션이름}:{태그네임}
access deny되면 도커 로그인하기
```

## 5. ec2(centOS) 환경설정
(1). 도커 설치
```
1. sudo yum install docker
```

(2). 도커 실횅
```
sudo systemctl start docker
```

(3). 도커 이미지 받기
```
sudo docker pull {도커사용자이름}/{애플리케이션이름}:{태그네임}
```

(4). 도커 이미지 실행
```
sudo docker run -p 8080:8080 {도커사용자이름}/{애플리케이션이름}
```

