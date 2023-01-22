# LogBack

### Appender 
- ConsoleAppender: 콘솔에 log를 출력
- FileAppender: 파일 단위로 log를 저장
- RollingFileAppender: 설정옵션에 따라 log를 여러 파일로 나누어저장
- SMTPAppender: log를 메일로 전송 하여 기록
- DBAppender: log를 db로 저장

## logback-spring.xml
기본 스프링부트 로그설정
<img width="697" alt="image" src="https://user-images.githubusercontent.com/46700734/213848029-2740d980-528f-4caa-b640-3e12b84cb738.png">

해당 설정을 통해 스프링부트의 기본 로그 설정을 참조할 수 있음
logback 프로필 설정을 통해 각 프로필별 설정 구성 가능

logback-spring-local.xml
<img width="858" alt="image" src="https://user-images.githubusercontent.com/46700734/213848788-569f2766-90a5-492e-a8ca-ae90e274645c.png">
- appender를 통해 CONSOLE2 appender 추가
- 해당 appender는 ConsoleAppender
- 기존 CONSOLE appender는 console-appender.xml에 정의
- appender의 filter > level에 debug 레벨 정의 가능
- appender의 pattern을 통해 로그 메시지 정의 가능

--- 
## RollingFileAppender 사용하기
<img width="744" alt="image" src="https://user-images.githubusercontent.com/46700734/213849355-f19eafe3-b3d6-4753-979b-65b3f3c79635.png">

- <file> 어떤 파일에 해당 로그를 쌓을 건지를 정의 (logs폴더의 request1.log)
- <rollingPolicy> 파일이 어떤식으로 저장할지 정의
- fileNamePattern 파일 이름을 어떤식으로 저장할지
- maxFileSize 로그파일 최대 크기
- maxHistory 로그파일 최대 보관주기 단위 (일)
- outputPatternAsHeader: 로그가 어떤 패턴으로 쌓이는지 첫줄에 보여줌  
  ![image](https://user-images.githubusercontent.com/46700734/213872550-e9dcdcad-12d4-46c5-b2f8-d04a90faeadf.png)

---
## LogBack 변수만들기
 
### logback-variable.properties 파일 만들기
![image](https://user-images.githubusercontent.com/46700734/213872717-d41aeeab-9407-4df7-8c52-18d21104b534.png)
![image](https://user-images.githubusercontent.com/46700734/213873093-3983a4e1-edfd-473c-b9f0-060f3ecaeb65.png)
사용하는 곳에 property로 import 시켜주기

---
## MDC

- 멀티쓰레드 환경에서 로그를 남길 때 사용하는 개념
- 쓰레드별 값을 동적으로 가져오기 위해 사용 
  ![image](https://user-images.githubusercontent.com/46700734/213874204-5986dae4-7a71-4bfb-aaa1-865df0740898.png)
  ![image](https://user-images.githubusercontent.com/46700734/213874223-b7c420fb-aa0a-413f-8a9e-94c1a4d33409.png)ㅅ

---
## ERROR 로그만을 위한 appender
![image](https://user-images.githubusercontent.com/46700734/213901121-f47defbc-2f93-41aa-aa8d-fc19be89f1ce.png)
- filter 추가 이후 level에 error 입력
  
---
## 특정컨트롤러에서 로거만들기 
![image](https://user-images.githubusercontent.com/46700734/213901508-de1d15e4-9300-4d37-be52-bee36d5523af.png)
![image](https://user-images.githubusercontent.com/46700734/213901533-f0347aa7-41ba-4981-9eca-7744676b6a66.png)
![image](https://user-images.githubusercontent.com/46700734/213905674-421eeaab-2284-4159-9258-5ece10cd4b67.png)


---
