### 개발환경 maven, ec2(centOS)

## 1. 각종 툴 설치
```
sudo yum install wget
sudo yum install maven
sudo yum install git
sudo yum install docker

```

## 2. 젠킨스 패키지 설치하기
```
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum install jenkins
sudo systemctl start jenkins     //젠킨스데몬실행하기
sudo systemctl status jenkins
```


## 3. 젠킨스 방화벽규칙 8080포트 열어주기
## 4. 젠킨스 페이지접속
그림과 같이 비밀번호로 막혀있음  

![image](https://user-images.githubusercontent.com/46700734/185799833-b078558c-a9d1-4f60-baef-0eab5779b897.png)

젠킨스 비밀번호 복사
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

## 5. 추천 플러그인 선택
왼쪽 선택  
![image](https://user-images.githubusercontent.com/46700734/185799928-dba8f695-e70a-4edb-a9ab-04a7fcac069c.png)


## 6. Jenkins관리 > 플러그인 관리 > 설치가능탭 > Publish Over SSH 선택 후 재시작없이 설치하기 

## 7. 젠킨스의 공개키 개인키 쌍 만들기
```
ssh-keygen -t rsa -f ~/.ssh/id_rsa
cd .ssh // 경로들어가 공개키 개인키 확인 id_rsa(개인키) id_rsa.pub(공개키) 존재

```
## 8. 젠킨스의 공개키를 워커인스턴스에 등록하기
```
워커인스턴스에서 해당 키 저장하는 곳으로 들어가기
vi ~/.ssh/authorized_keys
2. 젠킨스 인스턴스의 id_rsa.pub 의 내용 삽입
```

## 9. Key폴더 권한 변경
```
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

## 10. 젠킨스에 개인키랑 워커 인스턴스추가하기 
* Jenkins관리 > 시스템설정 > Publish over SSH로 이동
* jenkins 인스턴스 안에서 개인키 복사
* Publish over SSH 안에 key에 개인키 삽입
```
vi ~/.ssh/id_rsa 
```

![image](https://user-images.githubusercontent.com/46700734/185800661-2b59705d-7a72-4e30-93cc-d79d25808d1d.png)

* name: 워커인스턴스 이름
* Hostname: 워커인스턴스의 내부IP
* Username: 워커인스턴스의 로그인한 계정 sgs1159
* Remote directory: 워커인스턴스의 홈 Directory (cd ~하고 pwd) ```(Ex) /home/sgs1159```

## 11. 배포스크립트작성
```
1. jenkins 대시보드에서 좌측상단 '새로운 item' 클릭
2. item이름 정의  ex)  ${인스턴스이름} deploy
3. Freestyle project 클릭
4. 빌드환경탭 > 빌드 후 조치 추가 > Set build artifacts over SSH 클릭
5. 빌드 후 조치 SSH Server Name에 워커인스턴스 등록
6. 고급(advanced) 탭에 Verbose output in console버튼 체크 (로그 자세하게출력)
7. exec command 탭에 
```
```
nohup docker run -p 8080:80 ${로그인계정}/${워커인스턴스이름} > /dev/null 2>&1 &
```
nohup, & 는 백그라운드 실행
> /dev/null 2>&1 표준에러를 표준출력으로 redirection하라

![image](https://user-images.githubusercontent.com/46700734/185801034-2e915573-57c5-40d8-ad7f-257923f37292.png)

## 12. 워커인스턴스에 docker 설정
```
sudo yum install docker
sudo systemctl start docker
sudo chmod 666 /var/run/docker.sock
```



