### 1. Jenkins > 프로젝트 > 구성 > 소스 코드 관리 git 클릭 후 
```
Repository URL 에 clone하는 git 주소 입력
Github hook trigger for GITScm polling 클릭
```

### 2. Jenkins > 프로젝트 > 구성 > 빌드 환경 > Add build step 클릭 후 Execute shell클릭
Execute shell command안에 다음과 같이 입력
```
chmod 544 ./mvnw
./mvnw clean package
```

 ### 3. 빌드 후 조치 
 Transfer Set안에서 
 * Source files: target/{애플리케이션이름}.jar
 * Remove prefix: target
 * exec command: 
```
 sleep 30
 sudo kill -15 $(sudo lsof -t -i:8080)
 nohup sudo java -jar {매플리케이션이름}.jar > nohup.out 2>&1 &
```

### 4. 각 인스턴스의 java process제거하기
```
ps -aux | grep java
sudo kill -9 {PID}
```

### 5. github repository > settings > Webhooks > add webhook 
 payload url입력(젠킨스 인스턴스 url)
 ```
 젠킨스외부IP주소/8080/github-webhook/
 http://30.12.333.444/8080/github-webhook/
 ```
 Content type: application/json으로 변경
 
 ### (exc)특정포트 사용 명령어 lsof, cent os에서는 sudo yum install -y lsof
 8080포트 프로세스를 모두 죽이는 방법
 ```
 sudo kill -15 $(sudo lsof -t -i:8080)
 ```
 
 
 
 

