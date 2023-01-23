## ec2 sudo 권한주기
1. sudo vi /etc/ssh/sshd_config
passwordAuthentication yes로 변경하기

ubuntu 권한주기
```
sudo su -
```
ubuntu 패스워드 변경
```
passwd ubuntu
```

ubuntu 재시작
```
sudo service ssh restart
```
