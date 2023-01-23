## man
- cli 명령어에 대한 상세한 정보를 제공
- ex) man telnet, man grep

## lsof
- 특정 포트에 정보 조회 가능
- ex) lsof -i:8000-8080 // range search 

## nslookup
- dns 값으로 ip 조회
- ex) nslookup naver.com
- ex) nslookup google.com

## telnet
- IP + PORT 조합으로 현재 내 네트워크환경에서 통신이 가능한지 체크
- ex) telnet IP PORT

## netstat
- 네트워크 상태확인 가능
- 
```
a: 모든 포트 리스트와 연결여부
n: 숫자주소를 보여줌
l: 열린 포트리스트
t: 사용되는 모든 TCP 포트리스트
```
- ex) netstat -anlt

## netstat state
- Listen: 클라이언트의 요청을 기다림
- ESTABLISHED: 클라이언트와 통신중
