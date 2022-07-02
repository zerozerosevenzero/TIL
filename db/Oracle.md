# oracle db접속
sqlpluc "/ as sysdba"

# 유저생성
create user c##scott
 identified by tiger;
 
 # 유저 권한 부여
 grant dba to c##scott;
 
 # 유저 접속
 connect c##scott/tiger
 
![image](https://user-images.githubusercontent.com/46700734/176989404-98aecacd-26a5-4469-b457-26358c0881ce.png)

