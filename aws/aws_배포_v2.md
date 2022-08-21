
# 환경변수와 bashrc
## 환경변수

### 변수정의방법

#### 임시저장
```
export LOVE="i love you"
echo $LOVE
```
#### 영구저장

* 저장
./bashrc 
```
  export LOVE="i love you"
  echo $LOVE
```

* 강제적용
``` 
  source ./.bashrc
  echo $LOVE 확인
```
 * * *
 
# 환경변수를 특정파일에만 적용하기

#!/bin/bash     sh대신에 bin/bash를 적용하겠다.

vi var.sh 만들고  안에 환경변수 설정
source ./var.sh 강제적용

deploy.sh에 실행권한주기
```
chmod u+x deploy.sh  
```
./deploy.sh로 deploy.sh 실행 -> 아무것도 안나옴

source ./var.sh 적용 후
./deploy.sh deploy.sh 실행 -> 'hello 출력

3. 환경변수 범위
.bashrc 어디에서나 사용가능
터미널 만들고 source적용 - 터미널이 꺼지기 직전까지
쉘 스크립트(파일)로 변수를 만들고 다른 파일에서 실행하기 위해서는

- .bashrc 등록되어 있던지
- source로 터미널에서 적용이 되어 있던지
- deploy.sh 파일이 실행되는 동안에만 변수를 사용할 수 있으면 된다.(파일에 source를 적용하자 ex) source ./var.sh)

* * *
## 재배포 고려하여 크론 종료
touch crontab_delete                    crontab_delete 빈폴더 생성
corntab crontab_delete                  crontab에 crontab_delete복사
rm crontab_delete
echo "2. cron delete complete"
* * *
서버 PID 찾아서 종료하기
ps -ef  -> 모든 프로세스 검색
pgrep -f bash  -> bash의 PID검색

프로젝트 setting.gradle 안에 프로젝트 이름정의 -> ex) aws-v2-0.0.1.jar 생성

## var.sh
```
GITHUB_ID="codingspecialist"
PROJECT_NAME="aws-v2"
PROJECT_VERSION="0.0.1" 
PROJECT_PID="$(pgrep -f ${PROJECT_NAME}-${PROJECT_VERSION}.jar)" 
JAR_PATH="${HOME}/${PRIJECT_NAME}/build/libs/${PROJECT_NAME}-${PROJECT_VERSION}.jar"  -> /home/ubuntu/aws-v2/build/libs/aws-v2-0.0.1.jar 

export GITHUB_ID 
export PROJECT_NAME 
export PROJECT_VERSION 
export PROJECT_PID
export JAR_PATH
```

prod환경으로 실행하기
```
java -jar -Dspring.profiles.active=prod aws-v2-0.0.1.jar
```

```
1>/dev/null 표준출력로그를 쓰레기통에
2>/dev/null 시스템에러로그를 쓰레기통에
```

* * *
```
nohup java -jar -Dspring.profiles.active=prod ${JAR_PATH} 1>log.out 2>err.out & 
```

포트확인
```
netstat -nlpt  
```
netstat 설치
```
sudo apt install net-tools 
```

실시간 로그를 보여줌
```
tail -f log.out  
```
* * *
crontab: 서버를 재시작하기위함 


cron 에 잘등록되었는지 확인 crontab -e
```
kill -9 21394
```

gradle을 빌드하려면 test파일이 있어야함
테스트없이 빌드하고 싶을 때 
```
./gradlew build -x test
```
* * *
파일 압축하기
-c tar로 압축할때
-v 압축을 하거나 풀 때 출력을 화면에 보여줄지 말지
-f 파일 이름 지정하기
-x tar로 압축풀때

1. 파일 압축 시 tar -cvf 원하는압축명 파일명 파일명
(ex)
```
 tar -cvf deploy.tar check-and-restart.sh deploy.sh var.sh
```
2. 파일 압축 풀기
tar -xvf 압축파일명
(ex)
```
 tar -xvf deploy.tar
```
새 ec2생성하고

ec2 생성시 ssh 접속버그 -> ssh-keygen -R url 

새 ec2생성하고
deploy.tar 전송
그리고 tar -xvf deploy.tar
./deploy.tar 실행















