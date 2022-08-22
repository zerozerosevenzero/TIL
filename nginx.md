## 개발환경 maven, ec2(centOS)환경 

### 1. Jenkins관리 > 시스템설정 > publish over ssh에 ec2 새 워커인스턴스 등록하기

### 2. Jenkins 인스턴스로 들어가 공개키 워커인스턴스에 등록하기
```
cat .ssh/id_rsa.pub
```
해당 공개키 각 워커인스턴스 .ssh/authorized_keys 안에 복사
```
vi .ssh/authorized_keys
```

### 3. 각 워커인스턴스 ssh파일 권한변경
```
chmod 600 ~/.ssh/authorized_keys
```

### (etc) GCP에서는 메타데이터 > ssh키(수정) > 공개키등록을 통해 공개키를 등록할 수 있음


### 4. Jenkins > 프로젝트로 > 구성 > 빌드 후 조치 탭 밑에 add server를 통해 서버를 추가 등록

### 5. 각 인스턴스 Exec command에 명령어 입력
```
nohup docker run -d -p 8080:80 sgs1159/application > nohup.out 2>&1 & 
```

### 6. nginx만들기
새로운 ec2에
```
sudo yum install nginx
sudo systemctl start nginx
```

### 7. nginx 설정 (로드밸런싱설정)
```
sudo vi /etc/nginx/nginx.conf

upstream {앱이름} {
  server {instance_1번의_ip}:8080 weight=100 max_fails=3 fail_timeout=3s;
  server {instance_2번의_ip}:8080 weight=100 max_fails=3 fail_timeout=3s;
  server {instance_3번의_ip}:8080 weight=100 max_fails=3 fail_timeout=3s;
}

location / {
  proxy_pass http://{앱이름};
  proxy_http_version 1.1;
  proxy_set_header Upgrade $http_upgrade;
  proxy_set_header Connection 'upgrade';
  proxy_set_header Host $host;
  proxy_cache_bypass $http_upgrade;
}
```

### 8. 위 설정이 완료되었으면 Nginx를 reload 시켜야함.
```
sudo systemctl reload nginx
```
### 9. Nginx의 에러로그를 확인하기 위한 명령어
```
sudo tail -f /var/log/nginx/error.log
```
### 10. nginx connect Fail에러를 해결할 수 있는 명령어
```
sudo setsebool -P httpd_can_network_connect on
```

