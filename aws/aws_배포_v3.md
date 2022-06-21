# 1. build
프로젝트 터미널에 ./gralew build 

# 2. elastic bean stalk ec2접속하기
ssh -i {}.pem ec2-user@ec2주소

#3 nginx가 들어간 폴더를 다찾음
sudo find / -name nginx

#4 nginx.conf 위치
cd /etc/nginx


# 6. nginx 주요설정
cd conf.d > elasticbeanstalk > 00_application.conf
```
location / {
    proxy_pass          http://127.0.0.1:5000;
    proxy_http_version  1.1;

    proxy_set_header    Connection          $connection_upgrade;
    proxy_set_header    Upgrade             $http_upgrade;
    proxy_set_header    Host                $host;
    proxy_set_header    X-Real-IP           $remote_addr;
    proxy_set_header    X-Forwarded-For     $proxy_add_x_forwarded_for;
}
```
/ 로 접근 시 http://127.0.0.1:5000로 가라
